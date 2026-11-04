```
```c
#define OFF LOW
#define ON HIGH
#define Button 15                                      // GPIO 14

int LEDs[] = {13, 12, 3, 2, 0, 9, 8};                 // GPIO 9,10,22,27,17,3,2
int Numbers[7] = {
                {0, 99},                              // Dummy
                {2, 99},                               // Display 1
                {12, 9,99},                            // Display 2
                {12, 2, 99},                          // Display 3
                {13, 0, 3, 8,99},                     // Display 4
                {13, 0, 3, 8, 2,99},                 // Display 5
                {13, 0, 12, 9, 8, 3,99}              // Display 6
                };

//
// Configure LED ports as outputs,turn OFF LEDs. Also configure the
// Button port as input
//
void Configure()
{
        char k;
        for(k = 0; k < 7; k++)
        {
                pinMode(LEDs[k], OUTPUT);
                digitalWrite(LEDs[k], OFF);
        }
        pinMode(Button, INPUT);
}

//
// Display data on ports
//
void All_Off()
{
        char j;
        for(j = 0; j < 7; j++)digitalWrite(LEDs[j], LOW);
}

//
// Start of MAIN program
//
int main(void)
{
        int dice, i,nlen;
        wiringPiSetup();
```
```