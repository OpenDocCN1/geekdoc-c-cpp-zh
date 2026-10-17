With that, the data in Characteristic can be set locally so a connected Central can read from it.

```
char* outputString* = "Hello World";

int stringLength = 12;

ble.gattServer().write(

    characteristic.getValueHandle(),

    outputString,

    stringLength

);
```

# Putting It All Together

Create a new sketch called ble_send_data and copy the following code into the new sketch.

This sketch sets the value of the Characteristic to a random string every 5 seconds.

# Example 7–1. ble_send_data/main.c

```
#include "mbed.h"

#include "ble/BLE.h"

/** User interface I/O */
```