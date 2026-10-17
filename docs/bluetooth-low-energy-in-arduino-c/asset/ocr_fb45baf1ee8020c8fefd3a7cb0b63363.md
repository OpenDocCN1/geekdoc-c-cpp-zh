```
void onCentralDisconnected(const Gap::DisconnectionCallbackParams_t *params)
{
    BLE::Instance().gap().startAdvertising();
    serial.printf("Central disconnected\r\n");
}
```

The output from the Serial monitor should resemble this when a Central connects, then disconnects from the Peripheral (Figure 5-3).

Central connected: 45:b5:7d:96:01:2f

Central disconnected

# Figure 3-4. Serial Output

Your Peripheral can now handle connections and disconnections. You can modify the callback functions turn on an LED, print something to screen, or anything else.

# Example code

The code for this chapter is available online at: https://github.com/BluetoothLowEnergyInCppWithnRFx/Chapter05