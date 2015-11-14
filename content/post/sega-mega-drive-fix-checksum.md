+++
title = "Sega Mega Drive Fix Checksum"
date = "2012-02-08"
slug = "sega-mega-drive-fix-checksum"
tags = [ "emulation" ]
description = "Sega Mega Drive Fix Checksum"
+++

Иногда после пропатчивания ROM'ов с консоли Sega Mega Drive / Sega Genesis игра отказывается запускаться показывая нам красный экран. Это означает что в роме неправильно проставлена контрольная сумма, которую необходимо исправить.

Для исправления контрольной суммы 2 года назад я написал на питоне программу SMD Fix Checksum которую и выкладываю.

![Screenshot](http://savepic.su/2563086.png)

Скачать можно по ссылке [http://pysmart.emu-mobi.com/files/smd_fix_checksum.py](http://pysmart.emu-mobi.com/files/smd_fix_checksum.py)

Зависимости - *python 2* и *pygtk*
