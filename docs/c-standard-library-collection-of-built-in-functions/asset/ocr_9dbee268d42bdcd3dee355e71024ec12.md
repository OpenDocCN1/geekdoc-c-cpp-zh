The following example shows the usage of setlocale() function.

```
#include <locale.h>
#include <stdio.h>
#include <time.h>

int main ()
{
    time_t currtime;
    struct tm *timer;
    char buffer[80];

    time( &currtime );
    timer = localtime( &currtime );

    printf("Locale is: %s\n", setlocale(LC_ALL, "en_GB"));
    strftime(buffer,80,"%c", timer );
    printf("Date is: %s\n", buffer);

    printf("Locale is: %s\n", setlocale(LC_ALL, "de_DE"));
    strftime(buffer,80,"%c", timer );
    printf("Date is: %s\n", buffer);

    return(0);
}
```

Let us compile and run the above program that will produce the following result:

```
Locale is: en_GB

Date is: Thu 23 Aug 2012 06:39:32 MST

Locale is: de_DE

Date is: Do 23 Aug 2012 06:39:32 MST
```

# struct lconv *localeconv(void)

# Description