```
buff[2] = data;
spiWrite(handle, buff,3);
}

//
// Start of MAIN program
//
int main(void)
{
    gpioInitialise();
    
    handle = spiOpen(channel, 1000000,0);
    configure();
    
    while(1)
    {
        send(MCP_GPIOA, 0);
        time_sleep(1);
        send(MCP_GPIOA, 1);
        time_sleep(1);
    }
}
```

Figure 8.9 Program SPILED3.c

# 8.4 • Summary

In this chapter, we learned how to interface and use SPI bus devices with Raspberry Pi projects.

In the next chapter, we will be focusing on the important topic of using Analogue-to-Digital converters (ADCs) in our Raspberry Pi projects.