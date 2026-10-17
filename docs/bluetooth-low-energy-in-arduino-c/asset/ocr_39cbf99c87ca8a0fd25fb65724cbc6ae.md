```
```cpp
WriteOnlyArrayGattCharacteristic<uint8_t, sizeof(commandValue)> \\
    commandCharacteristic(
        commandCharacteristicUuid,
        (uint8_t *)commandValue,
        GattCharacteristic::BLE_GATT_CHAR_PROPERTIES_WRITE);

static char responseValue[characteristicLength] = {0};
ReadOnlyArrayGattCharacteristic<uint8_t, sizeof(responseValue)> \\
    responseCharacteristic(
        responseCharacteristicUuid,
        (uint8_t *)responseValue,
        GattCharacteristic::BLE_GATT_CHAR_PROPERTIES_READ | \\
        GattCharacteristic::BLE_GATT_CHAR_PROPERTIES_NOTIFY
    );

// Set up custom service
GattCharacteristic *characteristics[] = {
    &commandCharacteristic,
    &responseCharacteristic
};

GattService customService(
    customServiceUuid, characteristics,
```
```