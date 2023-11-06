---
title: "Android NDK: How to use CMake and ndk-build together in one project"
date: "2020-10-08T19:15:30+03:00"
description: "Android NDK currently provides us with at least two ways to build native libraries: CMake and ndk-build. But if you specify two paths to the build scripts CMakeLists.txt and Android.mk in the build.gradle file, then Gradle will show an error 'More than one externalNativeBuild path specified' and will not compile anything. I will show one of the possible ways to solve this problem."
summary: "Android NDK currently provides us with at least two ways to build native libraries: CMake and ndk-build. But if you specify two paths to the build scripts CMakeLists.txt and Android.mk in the build.gradle file, then Gradle will show an error 'More than one externalNativeBuild path specified' and will not compile anything. I will show one of the possible ways to solve this problem."
tags: ["dev", "android"]
#categories: []
slug: "android-ndk-cmake-and-ndkbuild"
aliases: []
toc: false
draft: fals
translationKey: "android-ndk-cmake-and-ndkbuild"
---

Android NDK currently provides us with at least two ways to build native libraries: *CMake* and *ndk-build*.

You may need to use both build systems at the same time to compile some existing libraries. But if you specify two paths to the build scripts *CMakeLists.txt* and *Android.mk* in the *build.gradle* file, then Gradle will show an error *"More than one externalNativeBuild path specified"* and will not compile anything. I will show one of the possible ways to solve this problem.

The most obvious solution would be to use *CMake* by default and run *ndk-build* separately. But I don't want to run it manually every time, so in this article, we will use Gradle's ability to invoke external commands and configure *ndk-build* to run automatically during application build.

I created [a simple project on GitHub](https://github.com/btimofeev/android_cmake_and_ndkbuild) with two C libraries: one with a build script *CMakeLists.txt* and the other built via *Android.mk*. You can view the files in the [app/src/main/jni/](https://github.com/btimofeev/android_cmake_and_ndkbuild/tree/main/app/src/main/jni) directory.

In the [app/build.gradle](https://github.com/btimofeev/android_cmake_and_ndkbuild/blob/main/app/build.gradle) file we configure the library build via *CMake* in the usual way:

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

This will allow us to compile the first library via *CMake* by simply starting the build of the application. To build the second library using *ndk-build*, we have the following task at the end of the [app/build.gradle](https://github.com/btimofeev/android_cmake_and_ndkbuild/blob/main/app/build.gradle) file:

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

Tasks of *Exec* type are used to run external commands. We must assign the path to the command to the `executable` property. To do this, we get the path to the installed NDK in the first line and add the name *"/ndk-build"* to it. We also pass an array of arguments for the command in the `args` property:

- `NDK_LIBS_OUT` - the directory in which the libraries will be located after compilation. Here we specify the path *src/main/jniLibs* because the libraries from this directory are automatically included in the APK after compiling the project. You will also have to override the property *android.sourceSets.main.jniLibs.srcDirs* if you need to specify a different directory here.

- `APP_BUILD_SCRIPT` - specifies the path to our build script *Android.mk*

- `NDK_APPLICATION_MK` - specifies the path to the *Application.mk* file, where we put the compilation settings

We can run this task now with `gradle runNdkBuild` command. You will see the freshly compiled *\*.so* files in the *app/src/main/jniLibs* directory if the compilation was successful.

It's time to add automatic execution of this task during the project build. Add a line to the end of the [app/build.gradle](https://github.com/btimofeev/android_cmake_and_ndkbuild/blob/main/app/build.gradle) file to do this:

```groovy
preBuild.dependsOn runNdkBuild
```

Here we have indicated that starting the build of the project depends on our task, so *ndk-build* will run just before the build. You can run `gradle clean` and `gradle build` to make sure everything builds as it should.
