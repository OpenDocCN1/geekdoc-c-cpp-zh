| CHARACTER | MEANING | EXAMPLE |
| --- | --- | --- |
| U | Universal sortable full date/time | Thursday, April 5, 2063 7:23:45 PM |
| Y or y | Year month | April, 2063 |

> > **NOTE** The result given by the U format may seem a bit surprising because it gives the time as 7:23:45 PM instead of 1:23:45 PM. The reason is the U specifier automatically converts a local time into Coordinated Universal Time (UTC) before formatting. (UTC is the time at 0° longitude. It’s basically the same as Greenwich Mean Time or GMT.) On April 5, 2063, the time 1:23 PM in my time zone will be 7:23 PM in Greenwich.

The dateTime class also provides several methods that return the date’s value as a string formatted in the most common date and time formats. Table 14-6 summarizes the most useful of these methods and shows the results on my computer set up for US English. Your results will depend on how your computer is configured.

TABLE 14-6

| METHOD | FORMAT | EXAMPLE |
| --- | --- | --- |
| ToLongDateString | Long date (D) | Thursday, April 5, 2063 |
| ToLongTimeString | Long time (T) | 1:23:45 PM |
| ToShortDateString | Short date (d) | 4/5/2063 |
| ToShortTimeString | Short time (t) | 1:23 PM |
| ToString | General date and time (g) | 4/5/2063 1:23:45 PM |

> > **NOTE** As is the case with number formats, you should use the standard specifiers or the standard methods (such as ToLongDateString) whenever possible so your computer can display dates and times in the formats used by the computer’s locale.

# Custom Date and Time Formats

If the standard date and time formatting characters don’t do the trick, you can use a custom format. Table 14-7 summarizes the custom date and time formatting strings. Note that for many of the characters in this table, the uppercase and lowercase versions have different meanings.