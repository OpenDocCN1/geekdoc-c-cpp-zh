Therefore our leapYear() function could finally be rewritten as:

```
// leapYear4.c

int leapYear(int year) {
    return (!((year % 4) && (year % 100)) || !(year % 400));
}
```

The leapYear() function might be called from another function, perhaps main(), in the following way:

```
// leapYearCall1.c

int main(void) {
    int num;

    num = leapYear(1996);
    if (num == 1) {
        printf("Leap year. ");
    }
    else {
        printf("No leap year. ");
    }
    return 0;
}
```

But here's a better way to make the call:

```
// leapYearCall2.c

int main(void) {
    if (leapYear(1996)) {
        printf("Leap year. ");
    }
    else {
        printf("No leap year. ");
    }
}
```