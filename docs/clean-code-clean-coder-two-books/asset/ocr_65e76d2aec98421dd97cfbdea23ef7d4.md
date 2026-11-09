```
```java
410     if (isValidMonthCode(month)) {
411         throw new IllegalArgumentException(
412             "SerialDate.monthCodeToString: month outside valid range.");
413     }
414
415     final String[] months;
416
417     if (shortened) {
418         months = DATE_FORMAT_SYMBOLS.getShortMonths();
419     }
420     else {
421         months = DATE_FORMAT_SYMBOLS.getMonths();
422     }
423
424     return months[month - 1];
425 }
426
427 /**
428  * Converts a string to a month code:
429  * <p>
430  * This method will return one of the constants JANUARY, FEBRUARY, ...,
431  * DECEMBER that corresponds to the string. If the string is not
432  * recognised, this method returns -1.
433  *
434  * @param s the string to parse.
435  *
436  * @return <code>-1</code> if the string is not parseable, the month of the
437  *         year otherwise.
438  */
439 public static int stringToMonthCode(String s) {
440
441     final String[] shortMonthNames = DATE_FORMAT_SYMBOLS.getShortMonths();
442     final String[] monthNames = DATE_FORMAT_SYMBOLS.getMonths();
443
444     int result = -1;
445     s = s.trim();
446
447     // first try parsing the string as an integer (1-12)...
448     try {
449         result = Integer.parseInt(s);
450     }
451     catch (NumberFormatException e) {
452         // suppress
453     }
454
455     // now search through the month names...
456     if (result < 1 || result > 12) {
457         for (int i = 0; i < shortMonthNames.length; i++) {
458             if (s.equals(shortMonthNames[i])) {
459                 result = i + 1;
460                 break;
461             }
462         }
463         if (s.equals(monthNames[i])) {
464             result = i + 1;
465             break;
466         }
467     }
468 }
469
470     return result;
471 }
```
```