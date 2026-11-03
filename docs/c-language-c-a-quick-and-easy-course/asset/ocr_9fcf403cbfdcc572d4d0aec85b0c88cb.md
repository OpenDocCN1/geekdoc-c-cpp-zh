# Time functions

The default time.h header file has the nine functions that follow: asctime(), clock(), ctime(), difftime(), gmtime(), localtime(), mktime(), strftime() and time(). This first function, asctime(), provides an alphanumeric string (ASCII) containing day, month, hour, minute, second and year; ctime() produces the same string, but you can get the time in time(); strftime() produces a formatted string; clock() gives the number of ticks (18.2 per second) since the start of the program; the gmtime() function converts the time in the Greenwich mean time and difftime() gives the difference between two times. In the example of the item above the time() function takes as argument a NULL constant, the system pointer to null argument. Their types are declared as time_t or clock_t.

The mini-program below illustrates the use of time-functions.

```
main(){time_t in,fi;float i;double d;in=time(NULL);
for(i=1;i<5000000;i++){ fi=time(NULL);d=difftime(fi,in);
printf("\nTime: %0.1f seconds.",d);}
```

The strftime() function has the following syntax: size_t strftime(char *s, size_t, tam, const char *format, const *pthour tm): Printing s we have the string with the time information requested in *format. The function value is the number of characters in s. The replacement characters are the following :

| Spec1 | Description1 | Spec2 | Description2 |
|---|---|---|---|
| %a | abbreviated weekday | %p | AM or PM |
| %A | day of the week | %S | second (0-59) |
| %b | abbreviated month name | %U | week of the year (0-53) |
| %B | Month name | %w | day (0-6) |
| %c | local time and date | %W | week of the year (on Monday) |
| %d | day (1-31) | %x | date location representation |
| %H | hour (0-23) | %X | local representation of the hour |
| %I | hour (1-12) | %y | year (0-99) |
| %J | day of the year (1-366) | %Y | year (four digits) |
|  |  |  |  |