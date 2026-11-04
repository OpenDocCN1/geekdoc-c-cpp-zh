```
```c
//
// Conenctions between Raspberry Pi and LCD
//
#define D4 2
#define D5 3
#define D6 17
#define D7 27
#define RS 22
#define E 10

//
// Start of MAIN program
//
int main(void)
{
    int lcd;
    char CurrentDate[16], CurrentTime[12];
    struct tm* timeinfo;
    time_t timer;

    wiringPiSetupGpio();
    lcd = lcdInit(2, 16, 4, RS, E, D4, D5, D6, D7, 0, 0, 0, 0);
    lcdClear(lcd);

    while(1)
    {
        time(&timer);
        timeinfo = localtime(&timer);

        strftime(CurrentDate, 16, "%d-%b-%Y", timeinfo);
        strftime(CurrentTime, 12, "%H:%M:%S", timeinfo);

        lcdPosition(lcd, 0, 0);
        lcdPuts(lcd, CurrentDate);

        lcdPosition(lcd, 0, 1);
        lcdPuts(lcd, CurrentTime);
        delay(1000);
    }
}
```
```

Figure 6.9 Program LCDDateTime.c