calendar in the following format.

```
```c
static char *months[] = {
                         “January”,
                         “February”,
                         “March”,
                         “April”,
                         “May”,
                         “June”,
                         “July”,
                         “August”,
                         “September”,
                         “October”,
                         “November”,
                         “December”
                         };

main()
{
                 static int days[12]={31,28,31,30,31,30,31,31,30,31,30,31};
                 long int ndays, ldays, tydays;
                 int d, i,         m, fday, y;
                 char ch;
                 clrscr();
                 printf(“Enter year(1900 onwards)& month (number):”);
                 scanf(“%d %d”,&y,&m);
                         ndays = (y-1)*365;
                         ldays = (y-1)/4-(y-1)/100+(y-1)/400;
                         tydays = ndays+ldays;
                         if((y%100==0&&y%400)||(y%4==0&&y%100!=0))
                                  days[1]=29;
                         else
                                  days[1]=28;
                         d= days[m-1];
                         tydays = 0;
                         for(i=0; i<m-2; i++)
                                  tydays = tydays + days[i];

                         tdays = tydays + tdays;
                         fday = tdays%7;
                         cal(y, m, fday, d);
}
```
```