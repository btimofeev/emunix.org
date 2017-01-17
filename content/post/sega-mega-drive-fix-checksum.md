+++
title = "Sega Mega Drive Fix Checksum"
date = "2012-02-08"
slug = "sega-mega-drive-fix-checksum"
tags = [ "emulation" ]
description = "Sega Mega Drive Fix Checksum"
+++

Иногда после пропатчивания ROM'ов с консоли Sega Mega Drive / Sega Genesis игра отказывается запускаться показывая нам красный экран. Это означает что в роме неправильно проставлена контрольная сумма, которую необходимо исправить.

Для исправления контрольной суммы 2 года назад я написал на питоне программу SMD Fix Checksum которую и выкладываю.

![Скриншот программы](../../images/sega-mega-drive-fix-checksum/smdfix.png)

Скачать можно на [GitHub'е](https://github.com/btimofeev/smd_fix_checksum)

Зависимости - *python 2* и *pygtk*
