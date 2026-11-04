```
```c
//
int main(void)
{
    int dice;
    wiringPiSetup();
    Configure();

    while(1)
    {
        All_Off();
        while(digitalRead(Button) == 0);
        dice = (rand() % 6) + 1;    // 1 to 6
        switch(dice)
        {
        case 1:                     // Dice 1?
            digitalWrite(D4, HIGH);
            break;
        case 2:                     // Dice 2?
            digitalWrite(D2, HIGH);
            digitalWrite(D6, HIGH);
            break;
        case 3:                     // Dice 3?
            digitalWrite(D2, HIGH);
            digitalWrite(D4, HIGH);
            digitalWrite(D6, HIGH);
            break;
        case 4:                     // Dice 4?
            digitalWrite(D1, HIGH);
            digitalWrite(D3, HIGH);
            digitalWrite(D5, HIGH);
            digitalWrite(D7, HIGH);
            break;
        case 5:                     // Dice 5?
            digitalWrite(D1, HIGH);
            digitalWrite(D3, HIGH);
            digitalWrite(D4, HIGH);
            digitalWrite(D5, HIGH);
            digitalWrite(D7, HIGH);
            break;
        case 6:                     // Dice 6?
            digitalWrite(D1, HIGH);
            digitalWrite(D2, HIGH);
            digitalWrite(D3, HIGH);
            digitalWrite(D5, HIGH);
            digitalWrite(D6, HIGH);
            digitalWrite(D7, HIGH);
        }
    }
}
```
```