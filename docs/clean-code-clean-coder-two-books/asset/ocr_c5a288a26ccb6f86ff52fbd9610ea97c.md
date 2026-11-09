```
```java
public abstract java.util.Date toDate();

/**
 * Returns a description of the date.
 *
 * @return a description of the date.
 */
public String getDescription() {
    return this.description;
}

/**
 * Sets the description for the date.
 *
 * @param description the new description for the date.
 */
public void setDescription(final String description) {
    this.description = description;
}

/**
 * Converts the date to a string.
 *
 * @return a string representation of the date.
 */
public String toString() {
    return getDayOfMonth() + "-" + SerialDate.monthCodeToString(getMonth())
           + "-" + getYYYY();
}

/**
 * Returns the year (assume a valid range of 1900 to 9999).
 *
 * @return the year.
 */
public abstract int getYYYY();

/**
 * Returns the month (January = 1, February = 2, March = 3).
 *
 * @return the month of the year.
 */
public abstract int getMonth();

/**
 * Returns the day of the month.
 *
 * @return the day of the month.
 */
public abstract int getDayOfMonth();

/**
 * Returns the day of the week.
 *
 * @return the day of the week.
 */
public abstract int getDayOfWeek();

/**
 * Returns the difference (in days) between this date and the specified
 * "other" date.
 * <p>
```
```