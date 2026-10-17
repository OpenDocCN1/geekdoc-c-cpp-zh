```
onCentralConnected
);

// attach callback when centlal disconnects

blePeripheral.setEventHandler(
    BLEDisconnected,
    onCentralDisconnected
);

blePeripheral.setAdvertisedServiceUuid(service.uuid());

blePeripheral.addAttribute(service);

blePeripheral.addAttribute(commandCharacteristic);

blePeripheral.addAttribute(responseCharacteristic);

commandCharacteristic.setEventHandler(
    BLEWritten,
    onCharacteristicWritten
);

Serial.print("Starting ");

Serial.println(bluetoothDeviceName);

blePeripheral.begin();
}

void loop() {
```