
它们不再是原来的数字；它们作为符号传递。我可以使用IDE的“重命名”功能来更改名称或类型，而不必担心在代码某处遗漏了某个-1或-2，或某个`int`参数声明没有被良好描述。

第208行的描述字段似乎没有人使用。我连同它的访问器和修改器一起删除了[G9]。

我还删除了第213行的退化默认构造函数[G12]。编译器会为我们生成它。

我们可以跳过`isValidWeekdayCode`方法（第216–238行），因为我们在创建Day枚举时删除了它。

接下来是`stringToWeekdayCode`方法（第242–270行）。对方法签名没有太大补充的Javadoc只是些冗余[C3]，[G12]。这个Javadoc唯一的价值在于描述了-1返回值。然而，由于我们改用了Day枚举，这个注释实际上是错误的[C2]。该方法现在会抛出`IllegalArgumentException`。所以我删除了Javadoc。

我还删除了参数和变量声明中所有的`final`关键字。据我所知，它们没有真正的价值，只会增加混乱[G12]。消除`final`与某些传统智慧背道而驰。例如，Robert Simmons^6强烈建议我们“……在代码中到处使用`final`。”显然我不同意。我认为`final`有少数几个好的用途，比如偶尔的final常量，但除此之外，这个关键字增加的价值很少，反而造成了大量混乱。也许我这样感觉是因为`final`可能捕获的那类错误已经被我编写的单元测试捕获了。

我不喜欢`for`循环中重复的`if`语句[G5]（第259行和第263行），所以我用`||`运算符将它们连接成一个`if`语句。我还使用Day枚举来驱动`for`循环，并做了一些其他外观上的修改。

我意识到这个方法实际上不属于DayDate。它实际上是Day的解析函数。所以我将它移入了Day枚举。然而，这使Day枚举变得相当大。由于Day的概念不依赖于DayDate，我将Day枚举移出DayDate类，放到了它自己的源文件中[G13]。

我还将下一个函数`weekdayCodeToString`（第272–286行）移入`Day`枚举，并命名为`toString`。

```java
public enum Day {
    MONDAY(Calendar.MONDAY),
    TUESDAY(Calendar.TUESDAY),
    WEDNESDAY(Calendar.WEDNESDAY),
    THURSDAY(Calendar.THURSDAY),
    FRIDAY(Calendar.FRIDAY),
    SATURDAY(Calendar.SATURDAY),
    SUNDAY(Calendar.SUNDAY);

    public final int index;
    private static DateFormatSymbols dateSymbols = new DateFormatSymbols();

    Day(int day) {
        index = day;
    }

    public static Day make(int index) throws IllegalArgumentException {
        for (Day d : Day.values())
            if (d.index == index)
                return d;
        throw new IllegalArgumentException(
            String.format("Illegal day index: %d.", index));
    }

    public static Day parse(String s) throws IllegalArgumentException {
        String[] shortWeekdayNames =
            dateSymbols.getShortWeekdays();
        String[] weekDayNames =
            dateSymbols.getWeekdays();

        s = s.trim();
        for (Day day : Day.values()) {
            if (s.equalsIgnoreCase(shortWeekdayNames[day.index]) ||
                s.equalsIgnoreCase(weekDayNames[day.index])) {
                return day;
            }
        }
        throw new IllegalArgumentException(
            String.format("%s is not a valid weekday string", s));
    }

    public String toString() {
        return dateSymbols.getWeekdays()[index];
    }
}
```

有两个`getMonths`函数（第288–316行）。第一个调用第二个。第二个除了第一个之外从未被任何人调用。因此，我将这两个合并为一个，并大幅简化了它们[G9],[G12],[F4]。最后，我改了一个更具自描述性的名称[N1]。

```java
public static String[] getMonthNames() {
    return dateFormatSymbols.getMonths();
}
```

`isValidMonthCode`函数（第326–346行）因`Month`枚举而变得无关紧要，所以我删除了它[G9]。

`monthCodeToQuarter`函数（第356–375行）有特性依恋（FEATURE ENVY）^7的气味[G14]，可能应该作为名为`quarter`的方法放在`Month`枚举中。所以我替换了它。

```java
public int quarter() {
    return 1 + (index-1)/3;
}
```

这使`Month`枚举足够大，可以放入自己的类中。所以我将它移出`DayDate`，以与`Day`枚举保持一致[G11],[G13]。

接下来的两个方法名为`monthCodeToString`（第377–426行）。我们再次看到一个方法用标志调用其孪生方法的模式。将标志作为参数传递给函数通常是个坏主意，尤其是当该标志只是选择输出格式时[G15]。我重命名、简化并重构了这些函数，并将它们移入`Month`枚举中[N1],[N3],[C3],[G14]。

```java
public String toString() {
    return dateFormatSymbols.getMonths()[index - 1];
}
```

```java
public String toShortString() {
    return dateFormatSymbols.getShortMonths()[index - 1];
}
```

下一个方法是`stringToMonthCode`（第428–472行）。我重命名了它，将它移入`Month`枚举，并对其进行了简化[N1],[N3],[C3],[G14],[G12]。

```java
public static Month parse(String s) {
    s = s.trim();
    for (Month m : Month.values())
        if (m.matches(s))
            return m;
    try {
        return make(Integer.parseInt(s));
    }
    catch (NumberFormatException e) {}
    throw new IllegalArgumentException("Invalid month " + s);
}
```

```java
private boolean matches(String s) {
    return s.equalsIgnoreCase(toString()) ||
        s.equalsIgnoreCase(toShortString());
}
```

`isLeapYear`方法（第495–517行）可以表达得更清晰一些[G16]。

```java
public static boolean isLeapYear(int year) {
    boolean fourth = year % 4 == 0;
    boolean hundredth = year % 100 == 0;
    boolean fourHundredth = year % 400 == 0;
    return fourth && (!hundredth || fourHundredth);
}
```

下一个函数`leapYearCount`（第519–536行）实际上不属于`DayDate`。除了`SpreadsheetDate`中的两个方法外，没有人调用它。所以我将它下移了[G6]。

`lastDayOfMonth`函数（第538–560行）使用了`LAST_DAY_OF_MONTH`数组。这个数组实际上属于`Month`枚举[G17]，所以我将它移到了那里。我还简化了该函数，并使其更具表达力[G16]。

```java
public static int lastDayOfMonth(Month month, int year) {
    if (month == Month.FEBRUARY && isLeapYear(year))
        return month.lastDay() + 1;
    else
        return month.lastDay();
}
```

现在事情开始变得更有趣了。下一个函数是`addDays`（第562–576行）。首先，因为这个函数操作`DayDate`的变量，所以它不应该是静态的[G18]。因此我将其改为实例方法。其次，它调用了`toSerial`函数。这个函数应该重命名为`toOrdinal`[N1]。最后，这个方法可以被简化。

```java
public DayDate addDays(int days) {
    return DayDateFactory.makeDate(toOrdinal() + days);
}
```

`addMonths`（第578–602行）也是如此。它应该是一个实例方法[G18]。算法有点复杂，所以我使用了“解释性临时变量”（EXPLAINING TEMPORARY VARIABLES）^8[G19]来使其更透明。我还将方法`getMonthCode`重命名为`getMonth`[N1]。

```java
public DayDate addMonths(int months) {
    int thisMonthAsOrdinal = 12 * getYear() + getMonth().index - 1;
    int resultMonthAsOrdinal = thisMonthAsOrdinal + months;
    int resultYear = resultMonthAsOrdinal / 12;
    Month resultMonth = Month.make(resultMonthAsOrdinal % 12 + 1);

    int lastDayOfResultMonth = lastDayOfMonth(resultMonth, resultYear);
    int resultDay = Math.min(getDayOfMonth(), lastDayOfResultMonth);
    return DayDateFactory.makeDate(resultDay, resultMonth, resultYear);
}
```
