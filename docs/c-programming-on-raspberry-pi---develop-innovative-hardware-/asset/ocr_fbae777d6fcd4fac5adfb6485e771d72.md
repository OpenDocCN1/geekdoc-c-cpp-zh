```
```c
//
int main(void)
{
        wiringPiSetupGpio();
        count = 0;
        flag = 0;

        pullUpDnControl(Button, PUD_UP);        // Software pull-up
        wiringPiISR(Button, INT_EDGE_FALLING, &myISR);

        while(1)
        {
                if(flag == 1)
                {
                        flag = 0;
                        printf("count = %d\n", count);
                        while(digitalRead(Button) == 0);
                        delay(20);
                }
        }
}
```
```

Figure 12.5 Program EventInc2.c

# 12.3 • Project 2 – Using the tone library – generating 1kHz signal

# Description:

The tone library of wiringPi can be used to generate a software-controlled square wave signal on any pin of the Raspberry Pi with a maximum frequency of 5kHz (5000Hz). The frequency of the generated tone is not very accurate and can be used to generate tones on a piezo sounder (or a passive buzzer).

In this project, we will be generating a 1kHz tone on a passive buzzer.

# Block diagram:

Figure 12.6 shows the block diagram of the project.

![](bbox=[0.364, 0.772, 0.648, 0.879])

Figure 12.6 Block diagram of the project