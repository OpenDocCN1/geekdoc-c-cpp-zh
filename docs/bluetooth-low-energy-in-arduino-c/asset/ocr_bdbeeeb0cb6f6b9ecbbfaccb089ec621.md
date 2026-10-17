```
/**
* visually signal that program has not crashed
*/

void blinkHeartbeat(void);

/**
* Callback triggered when the ble initialization process has finished
*
* @param[in] params Information about the initialized Peripheral
*/

void onBluetoothInitialized(
    BLE::InitializationCompleteCallbackContext *params
);

/**
* Main program and loop
*/

int main(void) {
    serial.baud(9600);

    serial.printf("Starting Peripheral\r\n");

    ticker.attach(blinkHeartbeat, 1); // Blink status led every 1 second

    // initialized Bluetooth Radio
```