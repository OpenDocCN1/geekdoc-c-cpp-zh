The Minor numbers are typically unique between Major numbers, so that a user can track their movement around the grocery store using the iBeacon minor numbers for identification.

```
// Minor number identifies the iBeacon
```

```
static const uint16_t MINOR_NUMBER = 3344;
```

The transmission power is important in both in setting the range of the iBeacon and in allowing the Central to determine how close it is to an iBeacon

```
// radio transmission power
```

```
// 0xC8 = 200, 2's compliment is 256-200 = (-56dB)
```

```
static const uint16_t TRANSMISSION_POWER = 0xC8;
```

# Putting It All Together

The following sketch creates a Beacon Peripheral that stores its reference RSSI and x and y distances from some point in Characteristics. Implementing this is very easy; you’ve already done most of the work in the last few chapters.

Create a new sketch named ble_security and copy the following code.

Example 11-1. sketches/ble_beacon/ble_beacon.c