+++
title = "Тёмная сторона AsyncTask"
date = "2013-07-31"
slug = "the-dark-side-of-asynctask"
tags = [ "android", "dev" ]
description = "Тёмная сторона AsyncTask"
+++

*Это перевод статьи [The dark side of AsyncTask](http://bon-app-etit.blogspot.com/2013/04/the-dark-side-of-asynctask.html), автор Fr&#233; Dumazy.*

Привет всем,

В этой статье я хочу рассказать о некоторых проблемах [AsyncTask](http://developer.android.com/reference/android/os/AsyncTask.html). Я написал свою первую статью о том, как использовать AsyncTask примерно полгода назад. Теперь я собираюсь рассказать про проблемы, которые он может вызвать, о том как их можно исправить и о существующих альтернативах.

В настоящее время AsyncTask, вероятно, наиболее широко используемый на Android способ выполнения задач в фоне. С ним очень легко работать, за что AsyncTask и получил признание среди разработчиков. Но у этого класса есть несколько недостатков, о которых не все знают.

### Жизненный цикл
Существует небольшое непонимание работы AsyncTask. Вы можете думать, что, если Activity создавшая AsyncTask будет уничтожена, AsyncTask также будет уничтожен. Но это не так. AsyncTask продолжает работать, пока его метод *doInBackground()* не завершится. AsyncTask запустит метод *onCancelled(Result result)*, если мы отменяем задачу вызовом *cancel(boolean)*, либо метод *onPostExecute(Result result)*, если задача не была отменена.
<!-- TEASER_END -->
Предположим, наш AsyncTask не был отменен до того как Activity была уничтожена. Теперь, если AsyncTask попытается взаимодействовать с компонентами этой Activity программа упадет, т.к. Activity больше не существует. Таким образом, мы всегда должны быть уверены, что мы отменили нашу задачу до того как Activity будет уничтожена.  Метод *cancel(boolean)* требует один параметр: логическую переменную *mayInterruptIfRunning*. Она должна иметь значение true, если поток, выполняющий задачу должен прерваться, иначе задача имеет право выполниться до конца. Если в методе *doInBackground()* есть цикл, мы можем в нём проверять значение методом boolean *isCancelled()* для остановки дальнейшего выполнения задачи.

Таким образом, мы должны быть уверены, что AsyncTask всегда правильно отменяется. 

**Метод *cancel()* действительно работает?**  
**Короткий ответ:** иногда.  
Если вы вызовите *cancel(false)*, AsyncTask просто будет продолжать выполняться, пока не завершит свою работу, но метод *onPostExecute()* вызван не будет. Таким образом, мы позволяем нашему приложению делать бессмысленную работу. Вы скажете: давайте просто всегда вызывать *cancel(true)* и проблема решена, не так ли? Не совсем. *mayInterruptIfRunning* равный *true* постарается завершить задачу пораньше, но если наш метод непрерываемый, такой как *BitmapFactory.decodeStream()*, он все равно будет продолжать выполнять свою работу. Вы можете закрыть поток преждевременно и поймать выброшенное исключение, но это делает метод *cancel()* бессмысленным.

### Утечки памяти
Так как AsyncTask имеет методы, которые работают в фоновом потоке (*doInBackground()*), а также методы, которые работают в потоке пользовательского интерфейса (например *OnPostExecute()*), он сохраняет ссылку на Activity, до тех пор пока работает. Но, если Activity уничтожена, он будет по-прежнему хранить эту ссылку в памяти. Это совершенно бесполезно, потому что задача уже была отменена.

### Потеря результатов
Еще одной проблемой является то, что мы потеряем результаты выполнения AsyncTask если наша Activity будет пересоздана. Например, это происходит при повороте экрана. Activity будет уничтожена и создана заново, но наш AsyncTask теперь будет иметь недействительную ссылку на эту Activity, поэтому *onPostExecute()* не будет иметь никакого эффекта. Существует решение этой проблемы. Вы можете сохранять ссылку на AsyncTask во время изменения конфигурации (например, используя global holder в объекте Application). *Activity.onRetainNonConfigurationInstance()* и *Fragment.setRetainedInstance(true)* также могут помочь вам в этом случае.

### Последовательно или параллельно?
Существует много путаницы в том, как работают несколько AsyncTask: последовательно или параллельно. Всё дело в том, что его поведение было изменено несколько раз. Что я имею в виду под словами *"работают последовательно или параллельно"*? Предположим, где-то в коде у вас есть следующие строки:

```
new AsyncTask1().execute();
new AsyncTask2().execute();
```

**Будут ли эти две задачи выполняться одновременно или AsyncTask2 запустится после завершения работы AsyncTask1?**  
**Краткий ответ:** это зависит от версии API.

#### До API версии 1.6 (Donut):
В первой версии AsyncTask задачи выполнялись последовательно. Это значит, что следующая задача не будет запущена пока предыдущая не завершит свою работу. Это вызывало некоторые проблемы производительности. Одна задача должна ждать завершения другой. Не очень хороший подход.

#### С API версии 1.6 до API версии 2.3 (Gingerbread):
Разработчики Android решили изменить поведение так, что бы несколько AsyncTask могли работать параллельно в отдельных потоках. Но появилась другая проблема. Многие разработчики полагались на последовательное поведение, и вдруг у них возникло много проблем связанных с параллельным выполнением.

#### С API версии 3.0 (Honeycomb) по настоящее время
"М-да, разработчики, кажется, не пользуются этим? Давайте вернём всё как было." AsyncTask'и снова выполняются последовательно. Конечно, разработчики Android предоставили возможность выполнять задачи параллельно. Это делается методом *executeOnExecutor(Executor)*. Смотрите документацию для получения дополнительной информации по этому методу.

Если мы хотим быть уверены, что наши задачи выполняются параллельно, можно использовать следующий код:

```
public static void execute(AsyncTask as) {
	if (Build.VERSION.SDK_INT <= Build.VERSION_CODES.HONEYCOMB_MR1) {
		as.execute();
	} else {
  		as.executeOnExecutor(AsyncTask.THREAD_POOL_EXECUTOR);
	}
}
```
(Этот код не работает для API версий от 1 до 3)

### Нужен ли нам AsyncTask?
Не всегда. AsyncTask это простой способ выполнения фоновых задач без необходимости писать много кода, но как вы могли увидеть, если мы хотим чтобы все хорошо работало мы должны помнить о многих "подводных камнях". Другой способ асинхронной загрузки данных это использовние класса [Loaders](http://developer.android.com/guide/components/loaders.html). Он был введен в Android 3.0 (Honeycomb), а также доступен в *Android Support Library*. Смотрите документацию для получения дополнительной информации. Возможно, в ближайшем будущем, я напишу статью о том, как использовать Loaders, так что не забудьте зайти на мой блог позже (или на мой сайт [www.bon-app-etit.com](http://www.bon-app-etit.com)).