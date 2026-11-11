
## 第 6 章

## 日期与时间 API

### 本章内容

- 6.1 时间线，第 352 页
- 6.2 本地日期，第 355 页
- 6.3 日期调整器，第 358 页
- 6.4 本地时间，第 360 页
- 6.5 带时区时间，第 361 页
- 6.6 格式化和解析，第 365 页
- 6.7 与遗留代码互操作，第 369 页

光阴似箭，我们可以轻松地设定一个起点，并以秒为单位向前和向后计数。那么，为什么处理时间如此困难？问题出在人类身上。如果我们可以直接告诉彼此：“1523793600 见，别迟到！”一切都会变得简单。但我们希望时间与日光和季节相关。这就是事情变得复杂的地方。Java 1.0 有一个 Date 类，事后看来很天真，在 Java 1.1 引入 Calendar 类时，它的大多数方法都被弃用了。它的 API 并不出色，实例可变，而且没有处理闰秒等问题。第三次终于成功，Java SE 8 中引入的 java.time API 弥补了过去的缺陷，应该能在相当长一段时间内满足我们的需求。在本章中，你将了解是什么让时间计算如此令人烦恼，以及日期与时间 API 如何解决这些问题。

### 6.1 时间线

历史上，基本时间单位——秒——源自地球绕轴自转。一整圈有 24 小时，即 24 × 60 × 60 = 86400 秒，因此精确地定义一秒似乎只是天文测量的问题。不幸的是，地球会轻微晃动，因此需要更精确的定义。1967 年，根据铯-133 原子的固有属性，得出了与历史定义相符的新的精确秒定义。从那以后，一个原子钟网络负责维持官方时间。

官方计时机构会不时地将绝对时间与地球自转同步。起初，官方秒数会被略微调整，但从 1972 年开始，偶尔会插入“闰秒”。（理论上，偶尔可能需要删除一秒，但这种情况尚未发生。）有传言说要再次改变这一系统。显然，闰秒很麻烦，许多计算机系统转而使用“平滑”处理：在闰秒到来之前人为地减慢或加快时间，从而保持每天 86,400 秒。这种方法之所以有效，是因为计算机上的本地时间并没有那么精确，而且计算机习惯于与外部时间服务同步。

Java 日期与时间 API 规范要求 Java 使用这样的时间尺度：

- 每天有 86,400 秒。
- 每天中午与官方时间完全一致。
- 在其他时间以精确定义的方式与官方时间紧密匹配。

这使 Java 能够灵活地适应未来官方时间的变化。

在 Java 中，Instant 表示时间线上的一个点。一个称为纪元的原点被任意设定为 1970 年 1 月 1 日午夜，位于穿过伦敦格林尼治皇家天文台的本初子午线上。这与 UNIX/POSIX 时间使用的约定相同。从该原点开始，时间以每天 86,400 秒向前和向后计量，精确到纳秒。Instant 值最早可追溯到十亿年前（Instant.MIN）。这还不足以表示宇宙的年龄（约 135 亿年），但对于所有实际用途来说应该足够了。毕竟，十亿年前，地球被冰雪覆盖，居住着今天动植物的微观祖先。最大值 Instant.MAX 是公元 1,000,000,000 年 12 月 31 日。

静态方法 Instant.now() 给出当前时刻。你可以像往常一样使用 equals 和 compareTo 方法比较两个时刻，因此可以将时刻用作时间戳。

要找出两个时刻之间的差异，请使用静态方法 Duration.between。例如，下面展示了如何测量算法的运行时间：

```java
Instant start = Instant.now();
runAlgorithm();
Instant end = Instant.now();
Duration timeElapsed = Duration.between(start, end);
long millis = timeElapsed.toMillis();
```

Duration 是两个时刻之间的时间量。你可以通过调用 `toNanos`、`toMillis`、`getSeconds`、`toMinutes`、`toHours` 或 `toDays` 来获得 Duration 以常规单位表示的长度。

Duration 的内部存储需要的不仅仅是一个 long 值。秒数存储在 long 中，纳秒数存储在额外的 int 中。如果你想进行纳秒精度的计算，并且确实需要 Duration 的整个范围，可以使用表 6.1 中的某个方法。否则，你只需调用 `toNanos`，并使用 long 值进行计算。

> **注意：** 大约需要 300 年的纳秒才会使 long 溢出。

例如，如果你想检查一个算法是否至少比另一个快十倍，可以计算

```java
Duration timeElapsed2 = Duration.between(start2, end2);
boolean overTenTimesFaster =
    timeElapsed.multipliedBy(10).minus(timeElapsed2).isNegative();
// Or timeElapsed2.toNanos() < timeElapsed.toNanos() / 10
```

**表 6.1 时间点和 Duration 的算术运算**

| 方法 | 描述 |
|---|---|
| `plus`, `minus` | 将一个 Duration 加到此 Instant 或 Duration 上，或从此 Instant 或 Duration 中减去一个 Duration。 |
| `plusNanos`, `plusMillis`, `plusSeconds`, `minusNanos`, `minusMillis`, `minusSeconds` | 将给定时间单位的数量加到此 Instant 或 Duration 上，或从中减去。 |
| `plusMinutes`, `plusHours`, `plusDays`, `minusMinutes`, `minusHours`, `minusDays` | 将给定时间单位的数量加到此 Duration 上，或从中减去。 |
| `multipliedBy`, `dividedBy`, `negated` | 返回将此 Duration 乘以或除以给定 long 值，或乘以 -1 所得到的 Duration。注意只能缩放 Duration，不能缩放 Instant。 |
| `isZero`, `isNegative` | 检查此 Duration 是否为零或负数。 |

```java
public static void runAlgorithm()
{
    int size = 10;
    List<Integer> list = new Random().ints().map(i -> i % 100).limit(size)
        .boxed().collect(Collectors.toList());
    while (!IntStream.range(1, list.size()).allMatch(
            i -> list.get(i - 1).compareTo(list.get(i)) <= 0))
        Collections.shuffle(list);
    System.out.println(list);
}
```

### 6.2 本地日期

现在让我们从绝对时间转向人类时间。Java API 中有两种人类时间：*本地日期/时间* 和 *带时区时间*。本地日期/时间包含日期和/或一天中的时间，但没有关联的时区信息。本地日期的一个例子是 1903 年 6 月 14 日（λ 演算的发明者阿隆佐·丘奇出生的日子）。由于该日期既没有一天中的时间，也没有时区信息，因此它不对应于一个精确的时间点。相比之下，1969 年 7 月 16 日 09:32:00 EDT（阿波罗 11 号发射）是一个带时区的日期/时间，表示时间线上的一个精确时刻。

有许多计算不需要时区，在某些情况下，时区甚至可能成为障碍。假设你安排每周 10:00 开会。如果你在最后一个带时区时间上加 7 天（即 7 × 24 × 60 × 60 秒），并且恰好跨过夏令时边界，那么会议就会提前一小时或推迟一小时！

因此，API 设计者建议，除非你确实想表示绝对时间点，否则不要使用带时区时间。生日、节假日、日程时间等通常最好表示为本地日期或本地时间。

一个 `LocalDate` 是包含年、月、日的日期。要构造一个 `LocalDate`，可以使用 `now` 或 `of` 静态方法：

```java
LocalDate today = LocalDate.now(); // Today's date
LocalDate alonzosBirthday = LocalDate.of(1903, 6, 14);
alonzosBirthday = LocalDate.of(1903, Month.JUNE, 14);
// Uses the Month enumeration
```

与 UNIX 和 `java.util.Date` 中不规则的约定不同——其中月份从 0 开始，年份从 1900 开始计数——你需要提供一年中月份的常规数字。或者，你可以使用 `Month` 枚举。

表 6.2 展示了处理 `LocalDate` 对象最有用的方法。
