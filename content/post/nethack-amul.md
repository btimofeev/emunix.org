+++
title = "NetHack: Амулеты и их свойства"
date = "2016-02-27"
slug = "nethack-amul"
tags = [ "game", "nethack" ]
description = "Перевод классического nethack спойлера о амулетах"
+++


*© [amul-343.txt](https://nethackwiki.com/wiki/Amul-343.txt) Последний раз редактировалось 2004-02-06 для NetHack 3.4.3*   
*© Амулеты и их свойства в NetHack 3.4*  
*© Составлено для 3.2.2 Кевином Хьюго (Kevin Hugo).*  
*© Обновлено для 3.4.3 Диланом О'Доннеллом (Dylan O'Donnell).*  
*© Перевод с английского: Борис Тимофеев <btimofeev@emunix.org>*  
*Этот спойлер я перевёл для сайта [www.nethack-rutext.ru](http://www.nethack-rutext.ru/doku.php?id=wiki:amul-343ru). Здесь будет лежать его резервная копия.*

## Таблица амулетов

<center>

| АМУЛЕТ                      | ЦЕНА  | ВЕС | ВЕРОЯТНОСТЬ | СЪЕДОБЕН |
|-----------------------------|-------|-----|-------------|----------|
| amulet of change            | 150   | 20  | 130c        | ДА       |
| amulet of ESP               | 150   | 20  | 175         | ДА       |
| amulet of life saving       | 150   | 20  | 75          |          |
| amulet of magical breathing | 150   | 20  | 65          | ДА       |
| amulet of reflection        | 150   | 20  | 75          |          |
| amulet of restful sleep     | 150   | 20  | 135c        | ДА       |
| amulet of strangulation     | 150   | 20  | 135c        | ДА       |
| amulet of unchanging        | 150   | 20  | 45          | ДА       |
| amulet versus poison        | 150   | 20  | 165         | ДА       |
| imitation AoY               | 0     | 20  | 0           |          |
| Amulet of Yendor            | 30000 | 20  | 0           |          |

</center>
<!--more-->
Амулеты перечислены в алфавитном порядке.  Поле **ЦЕНА** обозначает базовую цену каждого амулета. **ВЕС** определяет вес (100 *zorkmid'ов* весит 1).

Амулеты составляют 1% всех случайно генерируемых вещей в основном подземелье, 1% в контейнерах, и 4% в аду.  **ВЕРОЯТНОСТЬ** это относительная вероятность каждого подтипа; суффикс показывает шанс благословенного/проклятого:

<center>

| суффикс | blessed | uncursed | cursed |
|---------|---------|----------|--------|
| c       | 0,5%    | 9%       | 90,5%  |
|         | 5%      | 90%      | 5%     |

</center>

Имитацию Амулета Йендора можно найти в кучах костей на уровне *Rogue* (50% шанс), у [клона](https://nethackwiki.com/wiki/Double_Trouble) Волшебника Йендора когда у вас нет настоящего Амулета (50% шанс), и у игроков-монстров на астральном плане (100%). Настоящий Амулет Йендора носит первосвященник(-ца) Молоха (*the high priest(ess) of Moloch*).

За исключением указанного ниже, вы можете контролировать эффекты, надевая и снимая амулет. Если в поле **СЪЕДОБЕН** стоит **ДА**, то можно получить постоянный эффект обратившись (путем полиморфа) в металлоеда (*rock mole*, *rust monster* или *xorn*) и съев амулет. Вероятность получения эффекта этим путём 1/5 (**"Magic spreads through your body as you digest the amulet."** - *"Магия распространяется по всему телу когда вы перевариваете амулет."*). Употребление в пищу **amulet of unchanging** не даёт неизменяемости, вместо этого возвращает вам вашу естественную форму ("un-change" you).

Описание первых девяти видов амулетов берётся произвольно из списка:

<center>

|            |           |           |
|------------|-----------|-----------|
| circular   | spherical | oval      |
| triangular | pyramidal | square    |
| concave    | hexagonal | octagonal |

</center>

И имитация и реальный Амулет Йендора появляются как **"Amulet of Yendor"**; их можно различать идентифицировав каждую отдельную копию, дать название настоящему, или положить каждый в контейнер (настоящий не поместится).  Возможно, найденная на уровне *Rogue* имитация Амулета всегда самоидентифицирована.

Ношение амулета ускоряет увеличение голода (см. [food-343.txt](http://www.nethack-rutext.ru/doku.php?id=wiki:eda_i_golod_nethack_3.4)).

## Эффекты амулетов
### amulet of change (амулет изменения)
 - Если его надеть или съесть, пол вашего персонажа изменится с мужского на женский и наоборот.  Пол имеет следующие эффекты в игре: 
   - Только монстры женского пола могут откладывать яйца.
   - Из яиц в инвентаре мужского персонажа могут вылупиться прирученные монстры.
   - Мужчин соблазняют суккубы, женщин соблазняют инкубы.
   - Нимфы "соблазняют" мужчин и "очаровывают" женщин.
   - Классы Cave(wo)man и Priest(ess) имеют разные имена (пещерный мужчина/пещерная женщина и священник/жрица).
   - Это определяет как к вам обращаются (чисто косметически).
 - Если вы обращены в однополого монстра, ваш базовый пол будет изменен, а не текущий, с тем исключением, что инкуб изменится в суккуба и наоборот.
 - **"You are suddenly very feminine/masculine!"** - *"Вы становитесь очень
   женственным/мужественным!"*
 - **"You don't feel like yourself."** - *"Вы не чувствуете себя как прежде"* (Обращены в однополого монстра, но базовый пол персонажа изменяется)
 - **"The amulet disintegrates!"** - *"Амулет распадается!"*

### amulet of ESP (амулет экстрасенсорного восприятия)
 - Если его надеть вы увидите монстров, имеющих разум, когда они находятся поблизости, или где-нибудь на уровне, если вы ослеплены.
 - Если его съесть телепатия работает только когда вы ослеплены.
 - Не отображает сообщений.

### amulet of life saving (амулет сохранения жизни)
 - Если его надеть, то ваша жизнь будет спасена, когда умрёте; при этом амулет распадается.
 - Не отображает сообщений, когда надеваешь.
 - Не даёт эффекта если его съесть.

### amulet of magical breathing (амулет магического дыхания)
 - Если его надеть или съесть вы получите свойства амфибии и можете задерживать дыхание.  Вы сможете плавать под водой и не сможете задохнуться или подавиться.
 - Не отображает сообщений.

### amulet of reflection (амулет отражения)
 - Если его надеть лучи от палочек, заклинаний и огнедышащие атаки могут быть отражены.
 - Не отображает сообщений, когда надеваешь.
 - Не даёт эффекта если его съесть.

### amulet of restful sleep (амулет спокойного сна)
 - Если его надеть или съесть вы заснёте в течение 1-100 ходов. Вы проснётесь в течение 1-20 ходов или если сон прервут.  Цикл будет повторяться если вы продолжите носить амулет.
 - Не отображает сообщений.

### amulet of strangulation (амулет удушения)
 - Если вы наденете амулет, то будете задушены за 6 ходов.  При попытке его съесть вы поперхнётесь, шанс выжить 1/20.  Исключения сделаны, если у вас есть эффект от амулета магического дыхания или polyself.
 - **"It constricts your throat!"** - *"Амулет стягивает ваше горло!"*

### amulet of unchanging (амулет неизменяемости)
 - Если его надеть, то он предотвращает изменение текущей формы полиморфом или другими
   средствами, а также защищает от превращения в слизь ([sliming](https://nethackwiki.com/wiki/Sliming)); любой процесс преобразования в слизь прекращается.
 - Не отображает сообщений когда надеваешь.
 - Если съесть, вы обращаетесь в свою естественную форму.

### amulet versus poison (амулет защиты от яда)
 - Если его надеть или съесть вы получите иммунитет к яду (*poison resistance*).
 - Не отображает сообщений.

### cheap plastic imitation of the Amulet of Yendor (дешёвая пластиковая имитация Амулета Йендора)
 - Не даёт эффекта и не отображает сообщений когда надеваешь.
 - Не может быть съеден.

### Amulet of Yendor (Амулет Йендора)
 - Когда Амулет у вас, вы получаете все следующие эффекты (в основном негативные):
    - Вы получаете [ясновидение](https://nethackwiki.com/wiki/Clairvoyance), если оно не заблокировано.
    - Для чтения заклинания необходимо больше энергии.
    - Голод увеличивается (дополнительно к эффекту голода от обычных амулетов).
    - Ускоряется тайм-аут удачи.
    - Сложность монстров зависит от самого глубокого уровня, которого вы достигли, а не от текущего уровня подземелья.
    - Меньше вероятность того, что монстры будут сгенерированы спящими.
    - При переходе на уровень выше в *Gehennom'е*, вас может телепортировать вниз на 0-3 уровня.  Вероятность зависит от вашей верности богу (*alignment: lawful, neutral, chaotic*):

<center>

| UP | L     | N     | C     |
|----|-------|-------|-------|
| +1 | 75.0% | 75.0% | 75.0% |
| 0  | 6.25  | 8.33  | 12.5  |
| -1 | 6.25  | 8.33  | 12.5  |
| -2 | 6.25  | 8.33  | 0.0   |
| -3 | 6.25  | 0.0   | 0.0   |

</center>

 - *(продолжение списка):*
    - Вы не можете телепортироваться на другой уровень.
    - Телепортация в пределах уровня блокируется 1/3 времени.
    - Волшебник может телепортироваться между уровнями (или в пределах уровня), чтобы найти вас.
    - Волшебник попытается украсть амулет.
    - Вам разрешается войти в Плоскость Земли (*the Plane of Earth*) поднявшись по лестнице или выпив **cursed potion of gain level** на 1-ом уровне подземелья.
    - Вы можете активировать порталы.
 - Если амулет надеть или вооружиться им, вы получите сообщение, что амулету становится *"жарче"*, по мере того как вы приближаетесь к магическому порталу.
 - Не отображает сообщений, когда надеваете.
 - Не может быть съеден. (После этого вы самого себя принесёте в жертву?)


## Благодарности

Благодарю Bruce Cox за вычитку исходной версии этого файла.  
За дальнейшие исправления и разъяснения Philipp Lucas, Jeff MacDonald, obscurity, Darshan Shaligram, Donald Welsh и Yoshi348.