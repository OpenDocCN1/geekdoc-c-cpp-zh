```
};

char rightarrow[8] = {
    0b00000,
    0b00100,
    0b0010,
    0b11111,
    0b0010,
    0b00100,
    0b00000,
    0b0000
};

//
// Display the custom character
//
void DisplayCustom(void)
{
    lcdCharDef(lcd, 0, uparrow);
    lcdCharDef(lcd, 1, downarrow);
    lcdCharDef(lcd, 2, leftarrow);
    lcdCharDef(lcd, 3, rightarrow);

    lcdClear(lcd);
    lcdPutchar(lcd, 0);
    delay(1000);
    lcdPutchar(lcd, 1);
    delay(1000);
    lcdPutchar(lcd, 2);
    delay(1000);
    lcdPutchar(lcd, 3);
    delay(5000);
}
//
// Start of MAIN program
//
int main(void)
{
    wiringPiSetupGpio();
    lcd = lcdInit(2, 16, 4, RS, E, D4, D5, D6, D7, 0, 0, 0, 0);
    DisplayCustom();
}
```

Figure 6.8 Program LCDcustom2.c