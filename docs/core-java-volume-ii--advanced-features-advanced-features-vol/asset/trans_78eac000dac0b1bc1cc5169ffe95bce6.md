
### DoubleSummaryStatistics 8（续）

- `(int | long | double) getMax()`
- `(int | long | double) getMin()`

返回已汇总元素的最大值或最小值；如果没有元素，则返回 `(Integer | Long | Double).(MAX | MIN)_VALUE`。

## 1.9 收集到映射中

假设你有一个 `Stream<Person>`，并希望将元素收集到一个映射中，以便之后可以通过 ID 查找人员。`Collectors.toMap` 方法有两个函数参数，分别生成映射的键和值。例如，

```java
    Map<Integer, String> idToName = people.collect(
        Collectors.toMap(Person::getId, Person::getName));
```

在常见情况下，如果值应当是实际元素，则对第二个函数使用 `Function.identity()`。

```java
    Map<Integer, Person> idToPerson = people.collect(
        Collectors.toMap(Person::getId, Function.identity()));
```

如果存在多个具有相同键的元素，就会发生冲突，收集器将抛出 `IllegalStateException`。你可以通过提供第三个函数参数来覆盖该行为，该参数根据现有值和新值来解决冲突并确定该键的值。你的函数可以返回现有值、新值或它们的组合。

这里，我们构造一个映射，对于可用区域设置中的每种语言，以它在你的默认区域设置中的名称（例如 "German"）作为键，以它的本地化名称（例如 "Deutsch"）作为值。

```java
    Stream<Locale> locales = Stream.of(Locale.getAvailableLocales());
    Map<String, String> languageNames = locales.collect(
        Collectors.toMap(
            Locale::getDisplayLanguage,
            loc -> loc.getDisplayLanguage(),
            (existingValue, newValue) -> existingValue));
```

我们不关心同一种语言可能出现两次（例如，德语在德国和瑞士），因此我们只保留第一个条目。

> **注意：** 在本章中，我使用 `Locale` 类作为有趣数据集的来源。有关使用区域设置的更多信息，请参见第 7 章。

现在假设我们想知道给定国家/地区中的所有语言。那么我们需要一个 `Map<String, Set<String>>`。例如，"Switzerland" 的值是集合 {French, German, Italian}。起初，我们为每种语言存储一个单元素集合。每当为给定国家/地区发现一种新语言时，我们就形成现有集合与新集合的并集。

```java
    Map<String, Set<String>> countryLanguageSets = locales.collect(
        Collectors.toMap(
            Locale::getDisplayCountry,
            l -> Collections.singleton(l.getDisplayLanguage()),
            (a, b) -> { // Union of a and b
                var union = new HashSet<String>(a);
                union.addAll(b);
                return union; }));
```

你将在下一节看到获得此映射的更简单方法。

如果你想要一个 `TreeMap`，请将构造函数作为第四个参数提供。你必须提供一个合并函数。下面是本节开头的一个示例，现在生成一个 `TreeMap`：

```java
    Map<Integer, Person> idToPerson = people.collect(
        Collectors.toMap(
            Person::getId,
            Function.identity(),
            (existingValue, newValue) -> { throw new IllegalStateException(); },
            TreeMap::new));
```

> **注意：** 对于每个 `toMap` 方法，都有一个等效的 `toConcurrentMap` 方法，它会生成一个并发映射。在并行收集过程中使用单个并发映射。当与并行流一起使用时，共享映射比合并映射更高效。请注意，元素不再按流顺序收集，但这通常不会有什么影响。

程序清单 1.5 中的程序给出了将流结果收集到映射中的示例。

### 程序清单 1.5 collecting/CollectingIntoMaps.java

```java
package collecting;

/**
 * @version 1.00 2016-05-10
 * @author Cay Horstmann
 */

import java.io.*;
import java.util.*;
import java.util.function.*;
import java.util.stream.*;

public class CollectingIntoMaps
{
   public static class Person
   {
      private int id;
      private String name;

      public Person(int id, String name)
      {
         this.id = id;
         this.name = name;
      }

      public int getId()
      {
         return id;
      }

      public String getName()
      {
         return name;
      }

      public String toString()
      {
         return getClass().getName() + "[id=" + id + ",name=" + name + "]";
      }
   }

   public static Stream<Person> people()
   {
      return Stream.of(new Person(1001, "Peter"), new Person(1002, "Paul"),
         new Person(1003, "Mary"));
   }

   public static void main(String[] args) throws IOException
   {
      Map<Integer, String> idToName = people().collect(
         Collectors.toMap(Person::getId, Person::getName));
      System.out.println("idToName: " + idToName);

      Map<Integer, Person> idToPerson = people().collect(
         Collectors.toMap(Person::getId, Function.identity()));
      System.out.println("idToPerson: " + idToPerson.getClass().getName()
         + idToPerson);

      idToPerson = people().collect(
         Collectors.toMap(Person::getId, Function.identity(),
            (existingValue, newValue) -> { throw new IllegalStateException(); },
            TreeMap::new));
      System.out.println("idToPerson: " + idToPerson.getClass().getName()
         + idToPerson);

      Stream<Locale> locales = Stream.of(Locale.getAvailableLocales());
      Map<String, String> languageNames = locales.collect(
         Collectors.toMap(
            Locale::getDisplayLanguage,
            l -> l.getDisplayLanguage(),
            (existingValue, newValue) -> existingValue));
      System.out.println("languageNames: " + languageNames);

      locales = Stream.of(Locale.getAvailableLocales());
      Map<String, Set<String>> countryLanguageSets = locales.collect(
         Collectors.toMap(
            Locale::getDisplayCountry,
            l -> Set.of(l.getDisplayLanguage()),
            (a, b) ->
            { // union of a and b
               Set<String> union = new HashSet<>(a);
               union.addAll(b);
               return union;
            }));
      System.out.println("countryLanguageSets: " + countryLanguageSets);
   }
}
```

## 1.11 下游收集器

`groupingBy` 方法生成一个映射，其值是列表。如果你想以某种方式处理这些列表，请提供一个下游收集器。例如，如果你想要集合而不是列表，可以使用你在上一节中看到的 `Collectors.toSet` 收集器：

```java
Map<String, Set<Locale>> countryToLocaleSet = locales.collect(
    groupingBy(Locale::getCountry, toSet()));
```

> **注意：** 在此示例以及本节其余示例中，我假设已静态导入 `java.util.stream.Collectors.*`，以便使表达式更易于阅读。

提供了几个收集器用于将收集的元素归约为数字：

- `counting` 生成已收集元素的计数。例如，它统计每个国家/地区有多少个区域设置。
- `summing(Int|Long|Double)` 接受一个函数参数，将该函数应用于下游元素，并生成它们的和。例如，它计算城市流中每个州的人口总和。
- `maxBy` 和 `minBy` 接受一个比较器，并生成下游元素的最大值和最小值。例如，它生成每个州最大的城市。

```java
Map<String, Long> countryToLocaleCounts = locales.collect(
    groupingBy(Locale::getCountry, counting()));
```

```java
Map<String, Integer> stateToCityPopulation = cities.collect(
    groupingBy(City::getState, summingInt(City::getPopulation)));
```

```java
Map<String, Optional<City>> stateToLargestCity = cities.collect(
    groupingBy(City::getState,
        maxBy(Comparator.comparing(City::getPopulation))));
```

`collectingAndThen` 收集器在收集器之后添加一个最终处理步骤。例如，如果你想知道有多少个不同的结果，请将它们收集到一个集合中，然后计算大小：

```java
Map<Character, Integer> stringCountsByStartingLetter = strings.collect(
    groupingBy(s -> s.charAt(0),
        collectingAndThen(toSet(), Set::size)));
```

