```
```java
 * @return The serial number of this date.
 */
public int toSerial() {
    return this.serial;
}

/**
 * Returns a <code>java.util.Date</code> equivalent to this date.
 *
 * @return The date.
 */
public Date toDate() {
    final Calendar calendar = Calendar.getInstance();
    calendar.set(getYYYY(), getMonth() - 1, getDayOfMonth(), 0, 0, 0);
    return calendar.getTime();
}

/**
 * Returns the year (assume a valid range of 1900 to 9999).
 *
 * @return The year.
 */
public int getYYYY() {
    return this.year;
}

/**
 * Returns the month (January = 1, February = 2, March = 3).
 *
 * @return The month of the year.
 */
public int getMonth() {
    return this.month;
}

/**
 * Returns the day of the month.
 *
 * @return The day of the month.
 */
public int getDayOfMonth() {
    return this.day;
}

/**
 * Returns a code representing the day of the week.
 * <p>
 * The codes are defined in the {@link SerialDate} class as:
 * <code>SUNDAY</code>, <code>MONDAY</code>, <code>TUESDAY</code>,
 * <code>WEDNESDAY</code>, <code>THURSDAY</code>, <code>FRIDAY</code>, and
 * <code>SATURDAY</code>.
 *
 * @return A code representing the day of the week.
 */
public int getDayOfWeek() {
    return (this.serial + 6) % 7 + 1;
}

/**
 * Tests the equality of this date with an arbitrary object.
 * <p>
```
```