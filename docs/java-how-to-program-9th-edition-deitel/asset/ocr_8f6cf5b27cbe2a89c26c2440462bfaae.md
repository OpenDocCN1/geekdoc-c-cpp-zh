# 1402 Appendix G Formatted Output

| Conversion suffix character | Description |
| --- | --- |
| e | Display the day of month without leading zeros (e.g., 3). |
| Y | Display the year with four digits (e.g., 2004). |
| y | Display the last two digits of the year with leading zeros (e.g., 04). |
| j | Display the day of the year with three digits, padding with leading zeros as necessary (e.g., 016). |

# Fig. G.7 | Date formatting conversion suffix characters. (Part 2 of 2.)

| Conversion suffix character | Description |
| --- | --- |
| H | Display hour in 24-hour clock with a leading zero as necessary (e.g., 16). |
| I | Display hour in 12-hour clock with a leading zero as necessary (e.g., 04). |
| k | Display hour in 24-hour clock without leading zeros (e.g., 16). |
| l | Display hour in 12-hour clock without leading zeros (e.g., 4). |
| M | Display minute with a leading zero as necessary (e.g., 06). |
| S | Display second with a leading zero as necessary (e.g., 05). |
| Z | Display the abbreviation for the time zone (e.g., EST, stands for Eastern Standard Time, which is 5 hours behind Greenwich Mean Time). |
| p | Display morning or afternoon marker in lowercase (e.g., pm). |
| P | Display morning or afternoon marker in uppercase (e.g., PM). |

# Fig. G.8 | Time formatting conversion suffix characters.

Figure G.9 uses the conversion characters t and T with the conversion suffix characters to display dates and times in various formats. Conversion character t requires the corresponding argument to be a date or time of type long, Long, Calendar (package java.util) or Date (package java.util)—objects of each of these classes can represent dates and times. Class Calendar is preferred for this purpose because some constructors

```
// Fig. G.9: DateTimeTest.java
// Formatting dates and times with conversion characters t and T.
import java.util.Calendar;

public class DateTimeTest
{
	public static void main( String[] args )
	{
		// get current date and time
		Calendar dateTime = Calendar.getInstance();
	}
```