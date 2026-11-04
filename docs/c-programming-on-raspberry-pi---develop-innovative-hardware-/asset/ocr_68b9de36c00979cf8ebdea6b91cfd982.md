```
~~~c
PI_THREAD(ThreadLEDB)
{
    while(1)
    {
        digitalWrite(LEDB, HIGH);
        delay(500);
        digitalWrite(LEDB, LOW);
        delay(500);
    }
}

//
// This thread flashes LEDC every 250ms
//
PI_THREAD(ThreadLEDC)
{
    while(1)
    {
        digitalWrite(LEDC, HIGH);
        delay(250);
        digitalWrite(LEDC, LOW);
        delay(250);
    }
}

//
// Start of MAIN program
//
int main(void)
{
    int t1, t2, t3;
    wiringPiSetupGpio();

    pinMode(LEDA, OUTPUT);            // LEDA is output
    pinMode(LEDB, OUTPUT);            // LEDB is output
    pinMode(LEDC, OUTPUT);            // LEDC is output

    t1 = piThreadCreate(ThreadLEDA);  // Start ThreadLEDA
    t2 = piThreadCreate(ThreadLEDB);  // Start ThreadLEDB
    t3 = piThreadCreate(ThreadLEDC);  // Start ThreadLEDC

    while(1);                         // Wait without exit
}
~~~
```

Figure 12.16 *Program MultiLED.c.*