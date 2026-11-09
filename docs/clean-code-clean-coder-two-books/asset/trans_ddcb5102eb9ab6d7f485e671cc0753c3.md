

```java
if ((day >= 1) && (day <= SerialDate.lastDayOfMonth(month, year))) {
    this.day = day;
}
else {
    throw new IllegalArgumentException("Invalid 'day' argument.");
}

// 序列号需要与年月日同步……
this.serial = calcSerial(day, month, year);

this.description = null;

}

/**
 * 标准构造函数——创建一个表示指定日期序号的新日期对象
 * （序号应在 2 到 2958465 之间）。
 *
 * @param serial 日期的序号（范围：2 到 2958465）。
 */
public SpreadsheetDate(final int serial) {

    if ((serial >= SERIAL_LOWER_BOUND) && (serial <= SERIAL_UPPER_BOUND)) {
        this.serial = serial;
    }
    else {
        throw new IllegalArgumentException(
                "SpreadsheetDate: Serial must be in range 2 to 2958465.");
    }

    // 年月日需要与序号同步……
    calcDayMonthYear();

}

/**
 * 返回附加到日期的描述。日期不一定要有描述，但对某些应用程序来说，
 * 描述是有用的。
 *
 * @return 附加到日期的描述。
 */
public String getDescription() {
    return this.description;
}

/**
 * 设置日期的描述。
 *
 * @param description 此日期的描述（允许 <code>null</code>）。
 */
public void setDescription(final String description) {
    this.description = description;
}

/**
 * 返回日期的序号，其中 1900 年 1 月 1 日 = 2
 * （这几乎与 Microsoft Excel for Windows 和 Lotus 1-2-3 中使用的
 * 编号系统一致）。
 *
 * @return 此日期的序号。
 */
public int toSerial() {
    return this.serial;
}

/**
 * 返回与此日期等价的 <code>java.util.Date</code>。
 *
 * @return 日期。
 */
public Date toDate() {
    final Calendar calendar = Calendar.getInstance();
    calendar.set(getYYYY(), getMonth() - 1, getDayOfMonth(), 0, 0, 0);
    return calendar.getTime();
}

/**
 * 返回年份（假设有效范围为 1900 到 9999）。
 *
 * @return 年份。
 */
public int getYYYY() {
    return this.year;
}

/**
 * 返回月份（一月 = 1，二月 = 2，三月 = 3）。
 *
 * @return 一年中的月份。
 */
public int getMonth() {
    return this.month;
}

/**
 * 返回一个月中的第几天。
 *
 * @return 一个月中的第几天。
 */
public int getDayOfMonth() {
    return this.day;
}

/**
 * 返回表示星期几的代码。
 * <p>
 * 这些代码在 {@link SerialDate} 类中定义为：
 * <code>SUNDAY</code>、<code>MONDAY</code>、<code>TUESDAY</code>、
 * <code>WEDNESDAY</code>、<code>THURSDAY</code>、<code>FRIDAY</code> 和
 * <code>SATURDAY</code>。
 *
 * @return 表示星期几的代码。
 */
public int getDayOfWeek() {
    return (this.serial + 6) % 7 + 1;
}

/**
 * 测试此日期与任意对象是否相等。
 * <p>
 * 如果对象是 {@link SerialDate} 基类的实例，并且它与此
 * {@link SpreadsheetDate} 表示同一天，则此方法返回 <code>true</code>。
 *
 * @param object  要比较的对象（允许 <code>null</code>）。
 *
 * @return 布尔值。
 */
public boolean equals(final Object object) {
    if (object instanceof SerialDate) {
        final SerialDate s = (SerialDate) object;
        return (s.toSerial() == this.toSerial());
    }
    else {
        return false;
    }
}

/**
 * 返回此对象实例的哈希码。
 *
 * @return 哈希码。
 */
public int hashCode() {
    return toSerial();
}

/**
 * 返回此日期与指定其他日期之间的差值（以天为单位）。
 *
 * @param other  要与之比较的日期。
 *
 * @return 此日期与指定其他日期之间的差值（以天为单位）。
 */
public int compare(final SerialDate other) {
    return this.serial - other.serial;
}

/**
 * 实现 Comparable 接口所要求的方法。
 *
 * @param other  另一个对象（通常是另一个 SerialDate）。
 *
 * @return 如果此对象小于、等于或大于指定对象，则返回负整数、零或正整数。
 */
public int compareTo(final Object other) {
    return compare((SerialDate) other);
}

/**
 * 如果此 SerialDate 表示与指定 SerialDate 相同的日期，则返回 true。
 *
 * @param other  要与之比较的日期。
 *
 * @return 如果此 SerialDate 表示与指定 SerialDate 相同的日期，则返回
 *         <code>true</code>。
 */
public boolean isOn(final SerialDate other) {
    return (this.serial == other.toSerial());
}

/**
 * 如果此 SerialDate 表示早于指定 SerialDate 的日期，则返回 true。
 *
 * @param other  要与之比较的日期。
 *
 * @return 如果此 SerialDate 表示早于指定 SerialDate 的日期，则返回
 *         <code>true</code>。
 */
public boolean isBefore(final SerialDate other) {
    return (this.serial < other.toSerial());
}

/**
 * 如果此 SerialDate 表示与指定 SerialDate 相同或早于指定 SerialDate 的日期，
 * 则返回 true。
 *
 * @param other  要与之比较的日期。
 *
 * @return 如果此 SerialDate 表示与指定 SerialDate 相同或早于指定 SerialDate 的日期，
 *         则返回 <code>true</code>。
 */
public boolean isOnOrBefore(final SerialDate other) {
    return (this.serial <= other.toSerial());
}

/**
 * 如果此 SerialDate 表示晚于指定 SerialDate 的日期，则返回 true。
 *
 * @param other  要与之比较的日期。
 *
 * @return 如果此 SerialDate 表示晚于指定 SerialDate 的日期，则返回
 *         <code>true</code>。
 */
public boolean isAfter(final SerialDate other) {
    return (this.serial > other.toSerial());
}

/**
 * 如果此 SerialDate 表示与指定 SerialDate 相同或晚于指定 SerialDate 的日期，
 * 则返回 true。
 *
 * @param other  要与之比较的日期。
 *
 * @return 如果此 SerialDate 表示与指定 SerialDate 相同或晚于指定 SerialDate 的日期，
 *         则返回 <code>true</code>。
 */
public boolean isOnOrAfter(final SerialDate other) {
    return (this.serial >= other.toSerial());
}

/**
 * 如果此 {@link SerialDate} 在指定范围内（包含端点），则返回
 * <code>true</code>。d1 和 d2 的日期顺序不重要。
 *
 * @param d1  范围的一个边界日期。
 * @param d2  范围的另一个边界日期。
 *
 * @return 布尔值。
 */
public boolean isInRange(final SerialDate d1, final SerialDate d2) {
    return isInRange(d1, d2, SerialDate.INCLUDE_BOTH);
}

/**
 * 如果此 SerialDate 在指定范围内，则返回 true（由调用者指定是否包含端点）。
 * d1 和 d2 的顺序不重要。
 *
 * @param d1 范围的一个边界日期。
 * @param d2 范围的第二个边界日期。
 * @param include 一个代码，控制范围的开始日期和结束日期是否包含在内。
 *
 * @return 如果此 SerialDate 在指定范围内，则返回 <code>true</code>。
 */
public boolean isInRange(final SerialDate d1, final SerialDate d2,
                         final int include) {
    final int s1 = d1.toSerial();
    final int s2 = d2.toSerial();
    final int start = Math.min(s1, s2);
    final int end = Math.max(s1, s2);

    final int s = toSerial();
    if (include == SerialDate.INCLUDE_BOTH) {
        return (s >= start && s <= end);
    }
    else if (include == SerialDate.INCLUDE_FIRST) {
        return (s >= start && s < end);
    }
    else if (include == SerialDate.INCLUDE_SECOND) {
        return (s > start && s <= end);
    }
    else {
        return (s > start && s < end);
    }
}

/**
 * 根据日、月、年计算序号。
 * <p>
 * 1900 年 1 月 1 日 = 2。
 *
 * @param d 日。
 * @param m 月。
 * @param y 年。
 *
 * @return 根据日、月、年计算出的序号。
 */
private static int calcSerial(final int d, final int m, final int y) {
    final int yy = (y == 1900) ? 365 : SerialDate.leapYearCount(y - 1);
    int mm = SerialDate.AGGREGATE_DAYS_TO_END_OF_PRECEDING_MONTH[m];
    if (m > MonthConstants.FEBRUARY) {
        if (SerialDate.isLeapYear(y)) {
            mm = mm + 1;
        }
    }
    final int dd = d;
```

