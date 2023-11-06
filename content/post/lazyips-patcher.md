+++
title = "Lazy IPS - небольшой IPS патчер для Linux"
date = "2023-11-06"
slug = "lazyips-patcher"
tags = [ "patcher", "linux", "emulation" ]
description = "Lazy IPS - небольшой IPS патчер для Linux"
+++

*Оригинальная заметка была написана в 2012 году, но потеряла актуальность, поэтому обновляю.*

<!--more-->

![Скриншот программы](https://github.com/btimofeev/lazy_ips/raw/master/img/screenshot.png#c)

Когда-то давно я написал программу для Symbian-телефонов применяющую патчи в формате IPS к ROM-файлам игр. Называлась она _pySmartIPS_ и была написана на Python 2.

В 2012 году на основе ее кода я сделал графическую утилиту _lazy-ips_ для линукса с использованием GTK2.

Еще через несколько лет мне начали присылать пулл реквесты: программу портировали на Python 3 и добавили возможность применять патчи из консоли, без запуска графического интерфейса. Также я добавил поддержку установки через setup.py

Скачать программу можно по адресу https://github.com/btimofeev/lazy_ips 

Для Arch Linux существует пакет в [AUR](https://aur.archlinux.org/packages/lazy-ips)
