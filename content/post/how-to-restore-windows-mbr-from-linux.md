+++
title = "Как восстановить Windows MBR из-под Linux"
date = "2011-11-03"
slug = "how-to-restore-windows-mbr-from-linux"
tags = [ "linux", "windows", "mbr", "cli" ]
description = "Как восстановить Windows MBR из-под Linux"
+++

Что делать если необходимо восстановить Windows Master Boot Record (MBR)? 

Берем любой LiveCD-дистрибутив linux и устанавливаем программу [ms-sys](http://ms-sys.sourceforge.net). К примеру, в Ubuntu для этого набираем в терминале:

```
sudo apt-get install ms-sys
```

Далее ищем в выводе следующей команды диск с установленной windows:

```
sudo fdisk -l
```

Если, например, таким диском является /dev/sda1, набираем:

```
sudo ms-sys -m /dev/sda
```

Вот и все, загрузчик восстановлен.
