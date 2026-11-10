```
```c
switch (option) {
    case 1: data_limit = 1; tariff = 255;
        break;
    case 2: data_limit = 2; tariff = 455;
        break;
    case 3: data_limit = 4; tariff = 755;
        break;
    case 4: data_limit = 10; tariff = 995;
        break;
    case 9: printf("Quitting ...\n");
        return 0;
    default: printf("Invalid option\n");
}

if (option >= 1 && option <= 4) {
    printf("You chose %d GB for Rs %d.\n", data_limit, tariff);
    printf("Cost per GB = Rs %.2f\n", (float) tariff / data_limit);
}
            /* Closes while */
}
```
```

PROGRAM 7.8: **mobile_tariffs.c**

```
```text
Choose from the following 4G plans:

    1. 1 GB for Rs 255
    2. 2 GB for Rs 455
    3. 4 GB for Rs 755
    4. 10 GB for Rs 995
    9. Exit
Enter choice: 4
You chose 10 GB for Rs 995.
Cost per GB = Rs 99.50

Choose from the following 4G plans:

    1. 1 GB for Rs 255
    2. 2 GB for Rs 455
    3. 4 GB for Rs 755
    4. 10 GB for Rs 995
    9. Exit
Enter choice: 9
Quitting ...
```
```

PROGRAM OUTPUT: **mobile_tariffs.c**

Observe how a multi-line menu of five options is created by a single **printf** statement with the aid of the `\t` and `\n` escape sequences. The user’s choice is used by **switch** to set the variables `data_limit` and `tariff`. This program terminates gracefully when the user selects 9.