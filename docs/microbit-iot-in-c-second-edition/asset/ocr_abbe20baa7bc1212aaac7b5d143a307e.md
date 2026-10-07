| Accelerometer | magnetometer (compass) |
|---|---||
| micro-bit V1.3 (MMA8653+MAG3110) | 0x1D (0x3A/03B) | 0x0E (0x1C/01D) |
| micro-bit V1.5 variant 1 (LSM303AGR) | 0x19 (0x32/033) | 0x1E (0x3C/03D) |
| micro-bit V1.5 variant 2 (FXOS8700CQ) | 0x1F (0x3E/03F) | 0x1F (0x3E/03F) |
| micro-bit V2.0 (LSM303AGR) | 0x19 (0x32/033) | 0x1E (0x3C/03D) |
| micro-bit V2.0 (FXOS8700CQ) | 0x1F (0x3E/03F) | 0x1F (0x3E/03F) |

The values in brackets are the shifted addresses for write/read.

# ## micro-bit V1.3

The accelerometer is a MMA8653 and you can find out how it works from its datasheet. It has I2C address 0xD. The magnetometer is a NXP MAG3110 and its datasheet reveals that it is I2C address 0xE0.

Of the two devices, the magnetometer is the simpler and so it provides a better introductory example. If you examine its datasheet you will find a table of registers:

| Name | Type | Address | Default | Comment |
|---|---|---|---|---|
| DR_STATUS | R | 0x00 | 0000 000 | Data status per axis |
| OUT X_MSB | R | 0x01 | (0x03) | Bits [15:8] of X measurement |
| OUT X_LSB | R | 0x02 | | Bits [7:0] of X measurement |
| OUT Y_MSB | R | 0x03 | (0x05) | Bits [15:8] of Y measurement |
| OUT Y_LSB | R | 0x04 | | Bits [7:0] of Y measurement |
| OUT Z_MSB | R | 0x05 | (0x07) | Bits [15:8] of Z measurement |
| OUT Z_LSB | R | 0x06 | | Bits [7:0] of Z measurement |
| WHO AM_I | R | 0x07 | 0xC4 | Device ID Number |
| SYSMOD | R | 0x08 | data | Current System |
| OFF X_MSB | R/W | 0x09 | 0000 000 | Bits [14:7] of user offset |
| OFF X_LSB | R/W | 0x0A | 0000 000 | Bits [6:0] of user X offset |
| OFF Y_MSB | R/W | 0x0B | 0000 000 | Bits [14:7] of user Y offset |
| OFF Y_LSB | R/W | 0x0C | 0000 000 | Bits [6:0] of user Y offset |
| OFF Z_MSB | R/W | 0x0D | 0000 000 | Bits [14:7] of user Z offset |
| OFF Z_LSB | R/W | 0x0E | 0000 000 | Bits [6:0] of user Z offset |
| DIE_TEMP | R | 0x0F | data | Temperature, signed 8 bits in C |
| CTRL_REG1 | R/W | 0x10 | 0000 0000 | Operation modes |
| CTRL_REG2 | R/W | 0x11 | 0000 0000 | Operation modes |