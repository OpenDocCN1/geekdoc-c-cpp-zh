Output of the preceding example is as follows:

```
```
The current time is Mon Mar 26 16:16:19 2012
```
```

# ## difftime()

The signature of the difftime() function is as follows:

```
```c
double difftime(time_t time2, time_t time1);
```
```

The difftime() function returns the difference in seconds between time1 and time2. Let's take an example of the difftime() function as mentioned in Listing 8.18:

Listing 8.18: Usage of difftime () function.

```
```c
#include<stdio.h>
#include<time.h>

int main()
{
    time_t t1,t2;
    long int count = 0;
    t1 = time(NULL);
    while( count <= 100000000) {
        count++;
    }
    t2 = time(NULL);
    printf("\n The difference in time is %f ",difftime(t2,t1));
    return 0;
}
```
```

Output of the preceding example is as follows:

```
```
The difference in time is 2.000000
```
```

# ## gmtime()

The gmtime() function returns a pointer to the time in the form of a structure. Time is represented in Coordinated Universal Time (UTC), which refers to Greenwich Meridian Time. The signature of the gmtime() function is as follows:

```
```c
struct tm *gmtime(const time_t *time);
```
```

The time pointer is received with the help of the time() function. If a system does not support UTC, then the function returns NULL. Let's take an example of the gmtime() function as mentioned in Listing 8.19:

Listing 8.19: Usage of gmtime () function.

```
```c
#include<stdio.h>
#include<time.h>

int main()
{
    struct tm *gmt;
    time_t t1;

    t1 = time(NULL);
    gmt = gmtime(&t1);

    printf("\n The UTC time is %s ",asctime(gmt));
    getch();
}
```
```