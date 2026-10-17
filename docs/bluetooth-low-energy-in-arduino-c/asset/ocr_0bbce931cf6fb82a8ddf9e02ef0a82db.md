```
```cpp
#include "mbed.h"
```
```

```
```cpp
#include "ble/services/iBeacon.h"
```
```

```
```cpp
/** User interface I/O **/
```
```

```
```cpp
// instantiate USB Serial
```
```

```
```cpp
Serial serial(USBTX, USBRX);
```
```

```
```cpp
// Status LED
```
```

```
```cpp
DigitalOut statusLed(LED1, 0);
```
```

```
```cpp
// Timer for blinking the statusLed
```
```

```
```cpp
Ticker ticker;
```
```

```
```cpp
/** Bluetooth Peripheral Properties **/
```
```

```
```cpp
// Bluetooth Peripheral Singleton
```
```

```
```cpp
// Beacon UUID - use the same UUID for a group of Beacons
```
```

```
```cpp
static const uint8_t UUID[] = {0xE2, 0x0A, 0x39, 0xF4, 0x73, 0xF5, 0x4B, 0xC4,
                                0xA1, 0x2F, 0x17, 0xD1, 0xAD, 0x07, 0xA9, 0x61};
```
```