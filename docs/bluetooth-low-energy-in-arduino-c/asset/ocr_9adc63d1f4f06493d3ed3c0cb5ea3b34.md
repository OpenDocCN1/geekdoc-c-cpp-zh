```
/** Functions **/

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
* This callback processes incoming writes to a Characteristic.
*
* @param[in] params
*   Information about the characterisitc being updated.
```