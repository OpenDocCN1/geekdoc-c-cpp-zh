If there is a device the function should return 0 and if there are no devices it should return 1:

```
int main()
{
    uBit.init();
    if (init() == 1) {
        uBit.serial.printf("No device \n\r");
    } else {
        uBit.serial.printf("Device detected \n\r");
    }
}
```

If you try this partial program using a logic analyzer with a 1-wire protocol analyzer you will see something like:

![](bbox=[0.118, 0.373, 0.832, 0.44375])

Seeing a presence pulse is the simplest and quickest way to be sure that your hardware is working.

# Writing Bits

Our next task is to implement the sending of some data bits to the device. The 1-Wire bus has a very simple data protocol. All bits are sent using a minimum of 60µs for each slot. Each slot must be separated from the next by a minimum of 1µs. The good news is that timing is only critical within each slot. You can send the first bit in a time slot and then take your time before you send the next bit, the device will wait for you. This means you only have to worry about timing within the functions that read and write individual bits.