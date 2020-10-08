---
title: "Andriod NDK: Как использовать CMake и ndk-build в одном проекте"
date: "2020-10-08T19:15:30+03:00"
description: "В настоящее время Android NDK предоставляет нам как минимум два способа сборки нативных библиотек: CMake и ndk-build. Проблема в том, что если вы попытаетесь использовать их совместно в одном проекте, то Gradle выдаст ошибку 'More than one externalNativeBuild path specified' и откажется собирать что-либо. В этой статье я покажу один из возможных путей решения этой проблемы."
summary: "В настоящее время Android NDK предоставляет нам как минимум два способа сборки нативных библиотек: CMake и ndk-build. Проблема в том, что если вы попытаетесь использовать их совместно в одном проекте, то Gradle выдаст ошибку 'More than one externalNativeBuild path specified' и откажется собирать что-либо. В этой статье я покажу один из возможных путей решения этой проблемы."
tags: ["dev", "android"]
#categories: []
slug: "android-ndk-cmake-and-ndkbuild"
aliases: []
toc: false
draft: false
translationKey: "android-ndk-cmake-and-ndkbuild"
---

В настоящее время Android NDK предоставляет нам как минимум два способа сборки нативных библиотек: *CMake* и *ndk-build*.

Вам может понадобиться использовать обе системы сборки одновременно для компиляции каких-то существующих библиотек. Но если в файле *build.gradle* указать два пути до сборочных скриптов *CMakeLists.txt* и *Android.mk*, то *Gradle* выдаст ошибку *"More than one externalNativeBuild path specified"* и откажется собирать что-либо. В этой статье я покажу один из возможных путей решения этой проблемы.

Самым очевидным решением будет использовать *CMake* по-умолчанию, а *ndk-build* запускать отдельно. Но я хочу, чтобы не было никаких лишних действий, поэтому в этой статье мы будем использовать возможность *Gradle* вызывать внешние команды и настроим автоматический запуск *ndk-build* во время сборки приложения.

В качестве примера к статье я создал [простейший проект на GitHub](https://github.com/btimofeev/android_cmake_and_ndkbuild) содержащий две библиотеки на C: одна со сборочным скриптом *CMakeLists.txt*, вторая собираемая через *Android.mk*. Посмотреть их вы можете в директории [app/src/main/jni/](https://github.com/btimofeev/android_cmake_and_ndkbuild/tree/main/app/src/main/jni).

В файле [app/build.gradle](https://github.com/btimofeev/android_cmake_and_ndkbuild/blob/main/app/build.gradle) настраиваем сборку библиотеки через *CMake* привычным способом:

```groovy
android {
    defaultConfig {
        ndk {
            abiFilters 'armeabi-v7a', 'arm64-v8a', 'x86', 'x86_64'
        }
    }

    externalNativeBuild {
        cmake {
            path "src/main/jni/cmake/CMakeLists.txt"
        }
    }
}
```

Это позволит нам скомпилировать первую библиотеку через *CMake* просто запустив сборку приложения. Чтобы собрать вторую библиотеку используя *ndk-build* напишем в конце файла [app/build.gradle](https://github.com/btimofeev/android_cmake_and_ndkbuild/blob/main/app/build.gradle) вот такую задачу:

```groovy
task runNdkBuild(type: Exec) {
    def ndkDir = android.ndkDirectory
    executable = "$ndkDir/ndk-build"
    args = ['NDK_PROJECT_PATH=build/intermediates/ndk',
            'NDK_LIBS_OUT=src/main/jniLibs',
            'APP_BUILD_SCRIPT=src/main/jni/ndkbuild/Android.mk',
            'NDK_APPLICATION_MK=src/main/jni/ndkbuild/Application.mk']
}
```

Как мы видим эта задача типа *Exec*, то есть она создана, чтобы запускать внешние команды. Свойству `executable` мы должны присвоить путь к команде. Для этого в первой строке получаем путь к установленному NDK и добавляем к нему название *"/ndk-build"*. В свойство `args` мы передаем массив аргументов для запускаемой команды, рассмотрим их подробнее:

- `NDK_LIBS_OUT` - каталог куда попадут библиотеки после компиляции (здесь мы указываем *src/main/jniLibs*, потому что библиотеки из этого каталога автоматически попадают в APK после компиляции проекта. Если вам нужно указать здесь другой каталог, то вам также придется переопределить *android.sourceSets.main.jniLibs.srcDirs*).

- `APP_BUILD_SCRIPT` - указываем путь к нашему сборочному скрипту *Android.mk*

- `NDK_APPLICATION_MK` - указываем путь к файлу *Application.mk*, в котором прописываем настройки компиляции.

Теперь можем запустить эту задачу командой `gradle runNdkBuild`. Если все прошло без ошибок, то вы увидите свежесобранные *\*.so* файлы в каталоге *app/src/main/jniLibs*. 

Пришло время добавить выполнение этой задачи во время компиляции проекта. Для этого дописываем в конец файла [app/build.gradle](https://github.com/btimofeev/android_cmake_and_ndkbuild/blob/main/app/build.gradle) строку:

```groovy
preBuild.dependsOn runNdkBuild
```

Здесь мы указали, что начало сборки проекта зависит от нашей задачи, поэтому *ndk-build* будет запускаться непосредственно перед сборкой. Можете выполнить `gradle clean` и `gradle build`, чтобы убедиться что все собирается как надо.
