+++
title = "NetHack: Раковины, питьё из них и пинание"
date = "2016-02-22"
slug = "nethack-sink"
tags = [ "game", "nethack" ]
description = "Перевод на русский язык спойлера о раковинах для игры NetHack"
summary = "Перевод на русский язык спойлера о раковинах для игры NetHack"
+++

*© [sink-343.html](https://nethackwiki.com/wiki/Sink-343.txt) Последняя редакция 2004-07-15 для NetHack 3.4.3*  
*© Составитель Дилан О'Доннелл ([Dylan O'Donnell](mailto:psmith@spod-central.org)).*  
*© Перевод в HTML Кейт Непвеу ([Kate Nepveu](mailto:knepveu@steelypips.org)); HTML ре-синхронизация 2005-08-29 Дэн Фабулич (Dan Fabulich).*  
*© Перевод с английского Борис Тимофеев <btimofeev@emunix.org>*  
*Этот спойлер я перевёл для сайта [www.nethack-rutext.ru](http://www.nethack-rutext.ru/doku.php?id=wiki:sink-343ru). Здесь будет лежать его резервная копия.*

## Питье из раковин

11/20: Нет эффекта. Появляется одно из следующих сообщений:

  + **"You take a sip of (very) <hot|warm|cold> water."** *("Вы выпиваете глоток (очень) <горячей|теплой|холодной> воды.")*

  + **"You hear clanking from the pipes..."** *("Вы слышите лязг из труб ...")*

  + **"You hear snatches of song from among the sewers..."** *("Вы слышите обрывки песни из канализационной трубы...")*
    
  + **"From the murky drain, a hand reaches up... --oops--"** *("Из темной канализации к вам тянется рука...")* (только при галлюцинациях)

1/20: Если у вас есть сопротивление огню - эффекта не будет; в противном случае вы потеряете **d6** очков жизни.

  + **"You take a sip of scalding hot water."** *("Вы выпиваете глоток обжигающе-горячей воды.")*

  + **"It seems quite tasty."** *("Кажется, довольно вкусно.")* (при наличии сопротевления огню)

1/20: Генерируется канализационная крыса (если не подвергались геноциду или не вымерли).

  + **"Eek! There's a sewer rat in the sink!"** *("Ой! В раковине сидит крыса!")* (не ослеплён)

  + **"Eek! There's something squirmy in the sink!"** *("Ой! В раковине что-то дёргается!")* (ослеплён)

  + **"The sink seems quite dirty."** *("Раковина выглядит совершенно грязной.")* (подвергались геноциду или вымерли)

1/20: Эффект подобен эффекту от выпитого случайного непроклятого зелья (за исключением зелья воды).

  + **"Some <potion appearance> liquid flows from the faucet."** *("<Описание зелья> жидкость течет из крана.")* (не ослеплён)

  + **"Some odd liquid flows from the faucet."** *("Необычная жидкость течет из крана.")* (ослеплён)

1/20: Если вам уже попадалось кольцо в этой раковине (путем питья или пинания) - эффекта не будет; в противном случае создается случайное кольцо и вы тренируете мудрость.

  + **"You find a ring in the sink!"** *("Вы нашли кольцо в раковине!")*

  + **"Some dirty water backs up in the drain."** (уже находили кольцо)

1/20: Раковина превращается в фонтан.

  + **"The pipes break! Water spurts out!"** *("Порыв трубы! Вода брызжет фонтаном!")*

1/20: Создается [Water Elemental](https://nethackwiki.com/wiki/Elemental#Water_elemental) (если не вымерли).

  + **"The water moves as though of its own will!"** *("Вода движется, как будто по своей воле!")*

  + **"But it quiets down."** *("Но утихает.")* (если вымерли)

1/20: Вы получаете одно очко опыта.

  + **"Yuk, this water tastes awful."** *("Фу, у воды отвратительный вкус.")*

1/20: Вас тошнит и ваше чувство голода увеличивается.

  + **"Gagg... this tastes like sewage! You vomit."** *("Уэээ... это вкус сточных вод! Вас вырвало.")*

1/20: Если вы не обращены в другой вид ([polymorph](https://nethackwiki.com/wiki/Polymorph)) - нет никакого эффекта; в противном случае вы изменяете вид.

  + **"This water contains toxic wastes!"** *("Эта вода содержит токсичные отходы!")*

  + **"You undergo a freakish metamorphosis!"** *("Вы испытываете причудливую трансформацию!")* (polymorph)


## Пинание раковин

4/5: **"Klunk! The pipes vibrate noisily."** *("Трубы шумно вибрируют.")* Тренирует ловкость.

1/5: Что-то еще, а именно:

  + Если вы еще не получили [black pudding](https://nethackwiki.com/wiki/Black_pudding) из раковины, есть шанс 1/3 что один будет сгенерирован и вы тренируете ловкость.

    + **"A <black> ooze gushes up from the drain!"** *("<Черная> грязь льется фонтаном из трубы!")* (не ослеплён)

    + **"You hear a gushing sound."** *("Вы слышите звук фонтана.")* (ослеплён)

  + Если вы не получили pudding и еще не было посудомойки, есть шанс 1/3 что одна будет призвана (инкуб, если женщина-гуманоид, суккуб, если мужчина гуманоид, иначе шансы равны), и вы тренируете ловкость.

    + **"The dish washer returns!"** *("Посудомойка возвращается!")* (не ослеплён)

    + **"Something returns!"** *("Что-то возвращается!")* (ослеплён)

  + Если вы не получили ничего из вышеперечисленного, есть шанс 1/3 что будет создано случайное кольцо (если вы его еще не получали из раковины), и вы тренируете мудрость и ловкость.

    + **"Flupp! Muddy waste pops up from the drain."** *("Грязные отходы всплывают из канализации.")* (не ослеплён)

    + **"Flupp! You hear a sloshing sound."** *("Вы слышите хлюпающий звук.")* (ослеплён)

    + **"You see a ring shining in its midst."** *("Вы видите кольцо, сияющее в раковине.")* (не ослеплён, кольцо создано)

  + Вы повредите ногу если не получили что-либо из вышеперечисленного. Ухудшаются характеристики ловкости и силы, есть шанс 1/3 причинить боль правой ноге на 5-10 ходов, и вы потеряете **d5** HP (**d3** HP если ваше телосложение больше 15).

    + **"Ouch! That hurts!"** *("Ой! Это больно!")*

## Другие эффекты

Если в воздухе над раковиной что-то есть, оно упадёт на пол: метательное оружие или вы во время левитации (причинит **d8 + 24 - CON** повреждений, плюс **d3** для каждого оружия или стопки оружия на клетке). 

Если бросить кольцо в раковину, то оно, как правило, пропадёт, при этом появится сообщение по которому можно идентифицировать кольцо; подробнее об этом написано в спойлере [Кольца и их основные свойства в NetHack 3.4](http://www.nethack-rutext.ru/doku.php?id=wiki:kolca_i_ix_osnovnye_svojstva_v_nethack_3.4/). 

Копая вниз на клетке с раковиной вы превратите ее в фонтан (**"The pipes break! Water spurts out!"**).

## Благодарности

Исправления и разъяснения предоставлены Topi Linkala и Seraph.
