# Registering a Common Handler

Instead of registering different signal handlers for each signal, we register a single signal handler for all sorts of signals. Listing 6.4 shows how to register a common handler:

**Listing 6.4: Registering a Common Handler**

```
```c
#include<stdio.h>
#include<signal.h>

void writeToFile(char *sigDec)
{
    FILE *fp = fopen("D:\\SignalTest.txt", "a");
    fprintf(fp,"\n %s Received ",sigDec);
    fclose(fp);
}

void sigHandler(int signum)
{
    switch(signum)
    {
        case SIGINT:writeToFile("SIGINT RECEIVED");
            break;
        case SIGTERM:writeToFile("SIGTERM RECEIVED");
            break;
        case SIGCONT:writeToFile("SIGCONT RECEIVED");
            break;
    }
}

int main()
{
    signal(SIGINT, (void*)sigHandler);
    signal(SIGTERM, (void*)sigHandler);
    signal(SIGCONT, (void*)sigHandler);

    while(1)
    {
        printf("\n Infinite Loop");
    }

    return 0;
}
```
```

In Listing 6.4, we have used a single signal handler while registering sigHandler() with the signal() function. When a signal is sent to the program, the registered signal handler will be called. If the program has registered the signal along with the signal handler, then the call to the signal handler will be made. Instead of keeping multiple signal handlers, the program keeps the same signal handler for all the signals registered. Depending on the type of signal, a specific task is carried out.

Next, let's discuss how to block a signal.