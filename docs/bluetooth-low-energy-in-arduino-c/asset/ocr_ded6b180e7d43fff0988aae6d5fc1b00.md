A response confirming the state of the LED to the Central is sent like this:

```
```cpp
void sendBleResponse(uint8_t ledState) {

    uint8_t responseValue[characteristicLength];

    responseValue[bleResponseFooterPosition] = \
        bleResponseConfirmationFooter;

    responseValue[bleResponseDataPosition] = ledState;

    BLE::Instance(BLE::DEFAULT_INSTANCE).gattServer().write(

        responseCharacteristic.getValueHandle(),

        (const uint8_t *)responseValue,

        characteristicLength);
}
```
```

# # Putting It All Together