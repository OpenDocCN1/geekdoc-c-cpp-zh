```
```c
send(handle, MCP_GPIOA_REG, 0);
delay(1000);
send(handle, MCP_GPIOA_REG, 1);
delay(1000);
}
}
```
```

*Figure 7.8 Program I2Cexpander2.c*

# ## 7.4 • Project 2 – EEPROM memory

# ### Description:

In this project, we will be using the I2C bus compatible 24LC256 type EEPROM memory chip and write characters ABCD to memory locations starting from address 0x1000 of memory. The data is then read from these locations and displayed on the PC screen to confirm write/read operation has been successful.

# ### Aim:

This project aims to show how an I2C based EEPROM memory can be programmed using Raspberry Pi and the C programming language.

# ### 24LC256 memory

The 24LC256 is a 32K x 8 (256 Kbit) EEPROM memory chip manufactured by Microchip Technology Inc. The chip can operate from 1.7V to 5.5V, having a standby current of 1µA and write current of 3mA. The chip can operate from 100kHz up to 1MHz. A hardware write protect pin is provided to disable writing to the chip. The 24LC256 is capable of both random and sequential reads up to 256K boundary. The device has a page write capability of up to 64 bytes of data. The device has 32768 addresses, ranging from 0x0000 to 0x7FFF Figure 7.9 shows the pin layout of the chip.

![](bbox=[0.378, 0.625, 0.616, 0.748])

*Figure 7.9 Pin layout of the 24LC256*

A0, A1, and A2 are used to set the LSB bits of the device I2C address. As shown below, the upper 4 bits of the device address are fixed at 1010 and the LSB bit is the R/W bit:

| 1 | 0 | 1 | 0 | A2 | A1 | A0 | R/W |
|---|---|---|---|---|---|---|---|