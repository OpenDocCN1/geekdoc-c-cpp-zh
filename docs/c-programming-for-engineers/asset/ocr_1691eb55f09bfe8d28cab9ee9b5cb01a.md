# 12.9 Hardware Access in Raspberry Pi

```
bcm2835_gpio_fsel(LED_PIN, BCM2835_GPIO_FSEL_OUTP);
```

```
// Declare pointer to GPIO register base address
volatile unsigned *gpio = (volatile unsigned *) BCM2835_GPIO_BASE;
```

```
while(1) {
```

```
// Use pointer to write 1 to GPIO pin, turn LED on
*gpio |= (1<<LED_PIN);
```

```
// Delay
delay(1000);
```

```
// Write 0 to GPIO pin to turn LED off
*gpio &= ~(1<<LED_PIN);
```

```
// Delay
delay(1000);
```

```
}
return 0;
}
```

In this example:

+   * We initialize the GPIO using the bcm2835 library. The bcm2835 library is a C library used for direct, low-level access to the GPIO (general-purpose input/output) on the Raspberry Pi's Broadcom 2835 SOC (system on a chip).
* Set GPIO pin 18 as an output pin.
* Declare a pointer to the GPIO register base address. The volatile keyword tells the compiler that the value in the register can be changed at any time external to the program.
* Inside the loop, we use the pointer to directly write to the GPIO register bitmask, toggling the LED on and off with delays between.

This direct access provides control over hardware components like LEDs. Pointers allow us to interact directly with physical GPIO ports, facilitating real-time interfacing with external devices on the Raspberry Pi.

# Summary

In this chapter, we have covered pointers to pointers, dynamic memory allocation, and some of the most commonly used functions for managing memory in C. By understanding these concepts, you'll be able to write more efficient and powerful C code, while avoiding common pitfalls and security risks.