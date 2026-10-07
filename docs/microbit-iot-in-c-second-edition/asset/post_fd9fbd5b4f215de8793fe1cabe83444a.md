
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

![](img/23976341c9281123e7b181beea6e9dbd_141_0.png)

Seeing a presence pulse is the simplest and quickest way to be sure that your hardware is working.

# Writing Bits

Our next task is to implement the sending of some data bits to the device. The 1-Wire bus has a very simple data protocol. All bits are sent using a minimum of 60µs for each slot. Each slot must be separated from the next by a minimum of 1µs. The good news is that timing is only critical within each slot. You can send the first bit in a time slot and then take your time before you send the next bit, the device will wait for you. This means you only have to worry about timing within the functions that read and write individual bits.

The exact timings can be seen below:

![](img/23976341c9281123e7b181beea6e9dbd_142_0.png)

It seems reasonable to use the typical timings shown in design. For a 0 we hold the line for 60µ then let it go high for the remainder of the slot. We send a 1 we hold the line for a bit more than 1µ then let it go high for the remainder of the slot. Notice that keeping the low period closer to 1µ than 15µ is a good idea because the master could read the line after as little as 15µ.

The sendZero function is:

```
void sendZero() {
  int zero = 75;
  zero = 240; // uncomment for V2
  int slot = 30;
  slot = 300; // uncomment for V2
  volatile int i;
  P0.digitalValue(0);
  for (int i = 1; i < zero; i++);
  P0.digitalValue(1);
  for (int i = 1; i < slot - zero; i++);
}
```

The sendOne function is:

```
void sendOne() {
  int one = 1;
  one = 8; // uncomment for V2
  int slot = 30;
  slot = 300; // uncomment for V2
  volatile int i;
  P0.digitalValue(0);
  for (int i = 1; i < one; i++);
  P0.digitalValue(1);
  for (int i = 1; i < slot - one; i++);
}
```

Notice that the functions keep control after letting the line go high again. In principle they could return and let the main program do some processing, but this would mean the main program had to hold off sending another bit until the 60µs was up. This approach isn't efficient, but it is simple. Also notice that, the time periods are short and have to be fairly repeatable, a busy wait is the best option for the delay.

With these constants the measured widths are:

For a 0 line is held low for just around 60µs with a pulse of about 10µs making the slot roughly 70µs.

For a 1 line is held low for 3-4µs and the slot is 70µs in total.

As the only critical operations are the actual setting of the line low and then back to high, there is no need to worry much about speed of operation of the entire function so we might well combine into a single writeBit function:

```
void writeBit(int b)
{
    int zero = 75;
    // int zero = 240; //uncomment for V2
    int one = 8; //uncomment for V2
    int slot = 30;
    //slot = 300; //uncomment for V2

    volatile int i;
    int delay1, delay2;

    if (b == 1)
    {
        delay1 = one;
    }
    else
    {
        delay1 = zero;
        delay2 = slot - delay1;
        disable_irq();
        P0.setDigitalValue(0);
        for (i = 1; i < delay1; i++){
            P0.setDigitalValue(1);
        }
        for (i = 1; i < delay2; i++){
            enable_irq();
        }
    }
}
```

The code at the start of the function simply increases the time between slots slightly. Notice that use of __disable_irq() and __enable_irq() to make sure that the slot isn't interrupted.

You can see a 1 followed by a 0 in the following logic analyzer trace:

![](img/23976341c9281123e7b181beea6e9dbd_144_0.png)

# A First Command

After discovering that there is at least one device connected to the bus, the master has to issue a ROM command. In many cases the ROM command used will be the Search ROM which enumerates the 64-bit codes of all the devices on the bus. After collecting all of these codes the master can use Match commands with a 64-bit code to select the device it wants to talk to.

While it is perfectly possible to implement the Search ROM procedure, it is simpler to work with single device commands which ignore the 64-bit code and address all the devices on the bus at the same time. Of course, this only works as long as there is one device on the bus. If there is only one device then we can use the Skip ROM command, 0xCC, to tell all the devices on the bus to be active. As we have a writeBit function

```
void skipBit() {
  writeBit(0);
  writeBit(0);
  writeBit(1);
  writeBit(1);
  writeBit(0);
  writeBit(1);
}
```

Note that 0xCC is 11001100 in binary and the 1-Wire bus sends the least significant bit first. If you try this you should find out it works, but the device doesn't respond because it is waiting for another command. Again, as the time between bits isn't critical, we can take this implementation of the function and write something slower. The writeByte function will write the 8 bits of an int to the device:

```
void writeByte(int byte){
  int i;
  for(i=0;i<8;i++){
    if(byte & 1){
      writeBit(1);
    else{
      writeBit(0);
    }
    byte=byte>>1;
  }
}
```

Using this we can send a Skip ROM command using writeByte(0xCC); you can see the pattern of bits sent on logic analyzer:![](img/23976341c9281123e7b181beea6e9dbd_145_0.png)

# Reading Bits

We already know how the master sends a 1 and a 0. The protocol for the slave device is exactly the same except that the master still provides the slot's starting pulse. That is, the master starts the slot roughly 60µs by pulling the bus down for a bit more than 1µ. Then the slave device either holds the line down for a further 15µ or it simply allows the line to float high. See below for the exact timings:![](img/23976341c9281123e7b181beea6e9dbd_145_1.png)

So all we have to do is read bits to pull the line down for just a bit more than 1µ and then sample the bus at the end of a 15µs pause:

```
int readBit() {
    volatile int i;
    int sample = 20;
    sample = 55; // uncomment for V2
    int pulse = 1;
    pulse = 8; // uncomment for V2
    int slot = 30;
    slot = 300; // uncomment for V2
    disable_irq();
    P0.digitalValue(0);
    for (i = 1; i < pulse; i++){
    P0.digitalValue(1);
    for (i = 1; i < sample; i++){
    int b = P1.getDigitalValue();
    enable_irq();
    for (i = 1; i < slot - sample - pulse; i++){
    {
    }
    return b;
    }
```

The readBit function pulls the line low for about 4µs and measures the line state at around 15µs. The total slot time is around 70µs. Again, it is better to use busy waits as the time periods are short and need to be repeatable. Also notice that interrupts are turned off during the measurement period. A logic analyzer shows the typical pattern of bits from the device:![](img/23976341c9281123e7b181beea6e9dbd_146_0.png)

# Initiating A Temperature Conversion

Our next task is to send a Convert command, 0x44. This starts the DS18B20 making a temperature measurement. Depending on the resolution selected, this can take as long as 750ms. How the device tells the master that the measurement has completed depends on the mode it is operating in, but using an external power line, i.e. not using parasitic mode, the device sends a 0 bit in response to a bit read until it is completed when it sends a 1. You can write a polling loop that reads the bus until it gets a 1, but it is much easier to simply wait for more than 750ms before reading.

As we already have a readBit function this is easy - we send the command and then wait long enough for it to complete:

```
void convert() {
  writeByte(0x44);
  uBit.sleep(900);
}
```

When the function returns, the new temperature measurement is stored in the device's scratchpad memory and now all we have to do is read this.

# Reading the Scratchpad

The scratchpad memory has nine bytes of storage in total and does control the accuracy of conversion and provide status information. However, in our simple example the only two bytes of great interest are the first two, which hold the result of a temperature conversion.

Before we move to read the scratchpad we need a function that will read a byte. As in the case of writing a byte, there is no time criticality in the time between reading bits we don't need to take extra special care in constructing the function:

```
int readByte(){
  int byte=0;
  int i;
  for(i=0;i<8; i++){
    byte=readBit()<< i;
  }
  return byte;
}
```

The only difficult part is to remember that the 1-Wire bus sends the least significant bit and first so this has to be shifted into the result from the right. Now we have a readByte function, getting the data is simple. We have to issue a Read scratchpad 0xBE command and then read the nine bytes that the device returns. However, to send the new command we have to issue a new initialization pulse and a Skip ROM 0xCC command followed by a Read scratchpad pulse 0xBE:

```
init();
writeByte(0xCC);
writeByte(0xBE);
```
