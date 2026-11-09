```
```java
/**
 * {@link SerialDate} base class, and it represents the same day as this
 * {@link SpreadsheetDate}.
 *
 * @param object  the object to compare (<code>null</code> permitted).
 *
 * @return A boolean.
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
 * Returns a hash code for this object instance.
 *
 * @return A hash code.
 */
public int hashCode() {
    return toSerial();
}

/**
 * Returns the difference (in days) between this date and the specified
 * other date.
 *
 * @param other  the date being compared to.
 *
 * @return The difference (in days) between this date and the specified
 *         other date.
 */
public int compare(final SerialDate other) {
    return this.serial - other.serial;
}

/**
 * Implements the method required by the Comparable interface.
 *
 * @param other  the other object (usually another SerialDate).
 *
 * @return A negative integer, zero, or a positive integer as this object
 *         is less than, equal to, or greater than the specified object.
 */
public int compareTo(final Object other) {
    return compare((SerialDate) other);
}

/**
 * Returns true if this SerialDate represents the same date as the
 * specified SerialDate.
 *
 * @param other  the date being compared to.
 *
 * @return <code>true</code> if this SerialDate represents the same date as
 *         the specified SerialDate.
 */
```
```