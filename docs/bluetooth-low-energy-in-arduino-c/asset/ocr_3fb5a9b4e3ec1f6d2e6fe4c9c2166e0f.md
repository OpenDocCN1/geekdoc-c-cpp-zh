```
```cpp
);

// allow connections

ble.gap().setAdvertisingType(

  GapAdvertisingParams::ADV_NON_CONNECTABLE_UNDIRECTED

);

// advertise every 1000ms

ble.gap().setAdvertisingInterval(1000); // 1000ms

// begin advertising

ble.gap().startAdvertising();


serial.printf(" done\r\n");

}
```
```

This sketch will create a Peripheral that advertises as “MyDevice.”
Nearby Centrals will see this Peripheral when scanning.

# # Example code

The code for this chapter is available online
at: [https://github.com/BluetoothLowEnergyInCppWithnRFx/Chapter04](https://github.com/BluetoothLowEnergyInCppWithnRFx/Chapter04)