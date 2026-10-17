```
```cpp
/** Build Service and Characteristic Relationships */

// Create a read/write/notify Characteristic
static uint8_t deviceNameCharacteristicValue[characteristicLength] = \\
    BROADCAST_NAME;

ReadOnlyArrayGattCharacteristic<uint8_t, sizeof(characteristicValue)> \\
    deviceNameCharacteristic(
        deviceNameCharacteristicUuid,
        characteristicValue);

static uint8_t modelNumberCharacteristicValue[characteristicLength] = \\
    modelNumber;

ReadOnlyArrayGattCharacteristic<uint8_t, sizeof(characteristicValue)> \\
    modelNumberCharacteristic(
        modelNumberCharacteristicUuid,
        characteristicValue);

static uint8_t serialNumberCharacteristicValue[characteristicLength] = \\
    serialNumber;

ReadOnlyArrayGattCharacteristic<uint8_t, sizeof(characteristicValue)> \\
```
```