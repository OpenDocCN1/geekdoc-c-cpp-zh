```
```cpp
if(error != BLE_ERROR_NONE) {
    return;
}

// Ensure that it is the default instance of BLE
if(ble.getInstanceID() != BLE::DEFAULT_INSTANCE) {
    return;
}

serial.printf("Describing Peripheral...");

// advertising parameters
ble.gap().accumulateAdvertisingPayload(
    // Device is Peripheral only
    GapAdvertisingData::BREDR_NOT_SUPPORTED |
    // always discoverable
    GapAdvertisingData::LE_GENERAL_DISCOVERABLE
);

// broadcast name
ble.gap().accumulateAdvertisingPayload(
    GapAdvertisingData::COMPLETE_LOCAL_NAME,
    (uint8_t *)BROADCAST_NAME,
    sizeof(BROADCAST_NAME)
```
```