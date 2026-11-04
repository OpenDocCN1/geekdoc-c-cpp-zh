```
while(1)
{
    printf("\n\nEnter month: ");
    scanf("%d", &mon);
    if(mon < 1 || mon > 12)
        break;
    if(mon == 2)
    {
        printf("Enter Feb days: ");
        scanf("%d", &mon_days);
    }
    else if(mon==4 || mon == 6 || mon == 9 || mon == 11)
        mon_days = 30;
    else
        mon_days = 31;
    printf("Enter start day (1=Mon,7=Sun): ");
    scanf("%d", &day);
    printf("Mon\tTue\tWed\tThu\tFri\tSat\tSun\n");
    for(i = 1; i < day; i++) /* Add some spaces up to the first day of the month to format the output. */
        printf("\t");
    rows = 0;
    for(i = 1; i <= mon_days; i++)
    {
        printf("%d\t", i);
        if(i == 8-day+(rows*7))
        {
            printf("\n\n");
            rows++;
        }
    }
    return 0;
}
```

Comments: The if statement in the last for statement checks whether the last day of the week is reached or not. If it is, a new line character is added. The rows variable counts how many day rows have been displayed so far. For example, if the user enters 3 as the first month day (day = 3), the first new line character will be added when i becomes 8-day+(rows*7) = 8-3+(0*7) = 5. Next, rows becomes 1. The next new line characters will be added when i becomes 12, 19, and 26, respectively.

C.6.36 Write a program that simulates a theater's ticket office. Assume that the seats are 300. The program should display a menu to perform the following operations:

+   1. Buy a ticket. The cost is $15 for adults and $10 for minors. There is a 10% discount for the purchase of more than three tickets.