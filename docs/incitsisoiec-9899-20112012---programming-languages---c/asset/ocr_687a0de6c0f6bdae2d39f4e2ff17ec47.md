# Sun Sep 16 01:03:52 1973\n\0

The fields making up this string are (in order):

+   1. The name of the day of the week represented by timeptr->tm_wday using the following three character weekday names: Sun, Mon, Tue, Wed, Thu, Fri, and Sat.

+   2. The character space.

+   3. The name of the month represented by timeptr->tm_mon using the following three character month names: Jan, Feb, Mar, Apr, May, Jun, Jul, Aug, Sep, Oct, Nov, and Dec.

+   4. The character space.

+   5. The value of timeptr->tm_mday as if printed using the fprintf format "%2d".

+   6. The character space.

+   7. The value of timeptr->tm_hour as if printed using the fprintf format "%.2d".

+   8. The character colon.

+   9. The value of timeptr->tm_min as if printed using the fprintf format "%.2d".

+   10. The character colon.

+   11. The value of timeptr->tm_sec as if printed using the fprintf format "%.2d".

+   12. The character space.

+   13. The value of timeptr->tm_year + 1900 as if printed using the fprintf format "%4d".

+   14. The character new line.

+   15. The null character.

# Recommended practice

The strftime function allows more flexible formatting and supports locale-specific behavior. If you do not require the exact form of the result string produced by the asctime_s function, consider using the strftime function instead.

# Returns

The asctime_s function returns zero if the time was successfully converted and stored in the array pointed to by s. Otherwise, it returns a nonzero value.