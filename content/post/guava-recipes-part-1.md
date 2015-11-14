+++
title = "Guava - простые рецепты, делающие ваш Java код чище, часть 1"
date = "2014-04-23"
slug = "guava-recipes-part-1"
tags = [ "dev", "java" ]
description = "Guava - простые рецепты, делающие ваш Java код чище, часть 1"
+++

*Это перевод статьи [Guava - simple recipes to make your Java code cleaner, 1st part](http://onthejvm.blogspot.ru/2013/06/guava-simple-recipes-to-make-your-java.html), автор Lukasz Barc.*

   
Это статья для тех, кто не работал с библиотекой Guava. Просто несколько простых примеров которые вы можете использовать в своем коде.

#### 1. Вы можете использовать Optional вместо простого возврата null в некоторых случаях: 

Вместо:

```
/**
* Может вернуть null в некоторых случаях ... но это
* трудно запомнить
*/
public static String someMethod() {
    String returnValue = null;
    if (new Date().getTime() % 2 == 0) {
        returnValue = "time % 2 == 0";
    }
    return returnValue;
}

public static void main(String[] args) {
    String str = someMethod();
    str.contains("%"); // ошибка, если str == null
}
```
<!--more-->

используйте это:

```
/**
 * Явно показывает, что метод может
 * возвратить пустое (null) значение
 */
public static Optional< String > someMethod() {
    Optional< String > returnValue = Optional.absent();
    if (new Date().getTime() % 2 == 0) {
        returnValue = Optional.of(new String());
    }
    return returnValue;
}

public static void main(String[] args) {
    Optional< String > str  = someMethod();
    if(str.isPresent()) {
        // значение не равно null
    }
    // вы можете работать с полученным значением, либо со значением по умолчанию, если str == null
    str.or("default value").contains("%");
}
```

#### 2. Вы можете использовать firstNonNull из класса Objects библиотеки Guava вместо записи "if else"

Вместо:

```
public T foo() {
    ...
    ...
    if(first != null) {
        return first;
    } else {
        return second;
    }
}
```

используйте это:

```
import static com.google.common.base.Objects.firstNonNull;
...
public T foo() {
    ...
    ...
    return firstNonNull(first, second);
}
```

#### 3. Вы можете использовать методы из класса Strings библиотеки Guava для работы с пустыми или null строками

Вместо:

```
if(str == null) {
    str = "";
}

if("".equals(str)) {
    str = null;
}

if(str == null || str.length() == 0) {
    // null или пустая строка
}
```
используйте это:

```
import static com.google.common.base.Strings.*;
    
str = nullToEmpty(str);
str = emptyToNull(str);
if(isNullOrEmpty(str)) {
   // null или пустая строка
}
```

#### 4. Вы можете использовать Object.equals(a, b) для безопасной проверки на равенство

Вместо:

```
a.equals(b); // ошибка, если а == null
```

используйте это:

```
import static com.google.common.base.Objects.equal;
...
equal(a, null); // возвратит false
equal(null, null); // возвратит true
equal(a, b); // возвратит true если a == b
```

#### 5. Вы можете использовать Joiner для соединения строк

Вместо:

```
StringBuffer buffer = new StringBuffer();
for (String str : strs) {
    if (str != null) {
        buffer.append(str);
        buffer.append(", ");
    }
}
if (buffer.length() >= 2) {
    buffer.substring(0, buffer.length() - 2);
}
return buffer.toString();
```

используйте это:

```
import com.google.common.base.Joiner;
...
return Joiner.on(", ").skipNulls().join(strs);
```

#### 6. Вы можете использовать Splitter для разбиения строки

Вместо:

```
String str = "abc, bcd,, cde   ,zsa";
String[] split = str.split(",");

// Что делать с пробелами, пустыми строками? 
```

используйте это:

```
import com.google.common.base.Splitter;
...
Splitter.on(',')
        .trimResults()
        .omitEmptyStrings()
        .split("abc, bcd,, cde   ,zsa");
```

#### 7. Вы можете использовать Multiset для подсчета количества вхождений объекта

Вместо:

```
Map< String, Integer > countMap = new HashMap< String, Integer >();
for (String word : words) {
    if(!countMap.containsKey(word)) {
        countMap.put(word, 0);
    }
    countMap.put(word, countMap.get(word) + 1);
}
```

используйте это:

```
import com.google.common.collect.HashMultiset;
import com.google.common.collect.Multiset;
...
Multiset< String > wordsMultiset = HashMultiset.create();
wordsMultiset.addAll(words);
```

#### 8. Вы можете использовать Multimap вместо Map со значениями List или Set

Вместо:

```
Map< String, List< String > > languagesMap = new HashMap< String, List< String >>();
for (Programmer programmer : programmers) {
    if (languagesMap.get(programmer.getLanguage()) != null) {
        languagesMap.put(programmer.getLanguage(), new ArrayList< String >());
    }
    languagesMap.get(programmer.getLanguage()).add(programmer.getEmail());
}
```

используйте это:

```
import com.google.common.collect.HashMultimap;
import com.google.common.collect.Multimap;
...
Multimap< String, String > languagesMap = HashMultimap.create();
for (Programmer programmer : programmers) {
    languagesMap.put(programmer.getLanguage(), programmer.getEmail());
}
```

*... продолжение следует ...*

