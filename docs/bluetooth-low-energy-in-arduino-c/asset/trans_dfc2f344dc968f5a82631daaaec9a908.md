
```cpp
char uuid[32];

};

BleTransmission bleTransmissionData;

bool bleDataWritten = false; // true if data has been received

BLEService service("180C");

BLECharacteristic characteristic(

  "2A56",

  BLERRead | BLENotify | BLEWrite, // read, write, notify

  characteristicTransmissionLength

);

BLEPeripheral blePeripheral;

bool bleCharacteristicSubscribed = false; // true when a client subscribes

// When data is sent from the client, it is processed here inside a callback
// it is best to handle the result of this inside the main loop
void onBleCharacteristicWritten(BLECentral& central,
  BLECharacteristic &characteristic) {
  bleDataWritten = true;
  bleTransmissionData.uuid = characteristic.uuid();
  bleTransmissionData.length = characteristic.valueLength();
  // Since we are playing with strings, we must use strncpy
  strncpy(bleTransmissionData.data,
    (char*) characteristic.value(), characteristic.valueLength());
}

void setBleCharacteristicValue(char* output, int length) {
    characteristic.setValue((const unsigned char*) output, length);
}

void setup() {
    Serial.begin(9600); // open a Serial connection
    while (!Serial); // wait for Serial console to open
    blePeripheral.setLocalName(bluetoothDeviceName);
    blePeripheral.setAdvertisedServiceUuid(service.uuid());
    blePeripheral.addAttribute(service);
    blePeripheral.addAttribute(characteristic);
    // trigger onBleCharacteristicWritten when data is sent to the characteristic
    characteristic.setEventHandler(
        BLEWritten,
        onBleCharacteristicWritten
    );
    blePeripheral.begin();
}
void loop() {
    // if the bleDataWritten flag has been set, print out the incoming data
    if (bleDataWritten) {
        bleDataWritten = false; // ensure only happens once
```

```
Serial.print(bleTransmissionData.length);

Serial.print(" bytes sent to characteristic ");

Serial.print(bleTransmissionData.uuid);

Serial.print(": ");

Serial.println(bleTransmissionData.data);

// send out flow control message

setBleCharacteristicValue((char*) bleReadReceiptMessage,
    bleReadReceiptMessageLength);
}
}
```

运行草图时，外设会将收到的数据打印到串行监视器中，然后通知已连接的中央设备它已准备好接收更多数据（图 10-2）。

16 bytes sent to characteristic 2A56: this is a super

Ready for more data

16 bytes sent to characteristic 2A56: long message

Ready for more data

# 图 10-2. 串行监视器输出

# 示例代码

本章代码可在线获取，网址为：https://github.com/BluetoothLowEnergyInCppWithnRFx/Chapter10

# 第 11 章

# # 项目：iBeacon

信标可用于测距或空间感知。iBeacon 是一种特殊的信标类型，得到了行业的广泛支持。它支持某些标识 iBeacon 的数据，使跨平台的测距和空间感知变得更加容易。

由于无线电信号强度会随距离增加而自然衰减，蓝牙外设既可用于测距，也可用于空间感知。

# ## 测距

蓝牙信号可用于估算外设与中央设备之间的距离，因为无线电信号质量会随距离以可预测的方式下降。下图展示了信号如何随距离增加而下降（图 11-1）。

当附近 iBeacon 的距离和位置都已知时（图 11-2）。

![](img/d7b9d81704fe6839dbdc99a45736bfb5_134_0.png)

# 图 11-2. 房间内中央设备与 iBeacon 的位置示例

这是一个相当依赖数学计算的过程，但其基础全部是毕达哥拉斯定理。通过计算由所有 iBeacon 与中央设备的相对位置构成的三角形形状，就可以确定中央设备的位置（图 11-3）。

读取。通过查询所发现 iBeacon 的 Major 和 Minor 编号，可以知道用户位于博物馆特定楼层的某个房间。相关内容从博物馆的 API 获取并加载到智能手机应用中。

# 对 Peripheral 进行编程

每个 iBeacon 都使用一个 UUID 加上 Major 和 Minor 编号进行标识。

属于同一组织单元的 iBeacon 共享同一个 UUID。例如，属于同一家连锁杂货店的所有 iBeacon。

```
// Beacon UUID - use the same UUID for a group of Beacons
```

```
static const uint8_t UUID[] = {

    0xE2, 0x0A, 0x39, 0xF4, 0x73, 0xF5, 0x4B, 0xC4,

    0xA1, 0x2F, 0x17, 0xD1, 0xAD, 0x07, 0xA9, 0x61
};
```

Major 编号通常用于标识 iBeacon——具有相同用途的 iBeacon 通常具有相同的 Major 编号，例如用于标识该连锁店中的各家门店。

```
// Major Number identifies the iBeacon
```

```
static const uint16_t MAJOR_NUMBER = 1122;
```

Minor 编号通常在 Major 编号范围内是唯一的，这样用户就可以通过 iBeacon 的 Minor 编号来跟踪自己在杂货店内的活动轨迹。

```
// Minor number identifies the iBeacon
```

```
static const uint16_t MINOR_NUMBER = 3344;
```

发射功率很重要，它既用于设置 iBeacon 的广播范围，也用于让中央设备判断自身与 iBeacon 的距离。

```
// radio transmission power
```

```
// 0xC8 = 200, 2's compliment is 256-200 = (-56dB)
```

```
static const uint16_t TRANSMISSION_POWER = 0xC8;
```

# 整合所有内容

下面的草图创建了一个 Beacon 外设，它将其参考 RSSI 以及相对于某个点的 x、y 距离存储在特征值中。实现起来非常简单；在前几章中你已经完成了大部分工作。

创建一个名为 ble_security 的新草图，并复制以下代码。

示例 11-1. sketches/ble_beacon/ble_beacon.c

```
```cpp
#include "mbed.h"
```
```

```
```cpp
#include "ble/services/iBeacon.h"
```
```

```
```cpp
/** User interface I/O **/
```
```

```
```cpp
// instantiate USB Serial
```
```

```
```cpp
Serial serial(USBTX, USBRX);
```
```

```
```cpp
// Status LED
```
```

```
```cpp
DigitalOut statusLed(LED1, 0);
```
```

```
```cpp
// Timer for blinking the statusLed
```
```

```
```cpp
Ticker ticker;
```
```

```
```cpp
/** Bluetooth Peripheral Properties **/
```
```

```
```cpp
// Bluetooth Peripheral Singleton
```
```

```
```cpp
// Beacon UUID - use the same UUID for a group of Beacons
```
```

```
```cpp
static const uint8_t UUID[] = {0xE2, 0x0A, 0x39, 0xF4, 0x73, 0xF5, 0x4B, 0xC4,
                                0xA1, 0x2F, 0x17, 0xD1, 0xAD, 0x07, 0xA9, 0x61};
```
```

```
// Major Number and Minor number identify the Beacon

static const uint16_t MAJOR_NUMBER = 1122;

static const uint16_t MINOR_NUMBER = 3344;

// radio transmission power

// 0xC8 = 200, 2's compliment is 256-200 = (-56dB)

static const uint16_t TRANSMISSION_POWER = 0xC8;

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
```

```
/**
 * Main program and loop
 */

int main(void) {

    serial.baud(9600);

    serial.printf("Starting iBeacon\r\n");

    ticker.attach(blinkHeartbeat, 1); // Blink LED every 1 seconds

    // initialized Bluetooth Radio

    BLE &ble = BLE::Instance(BLE::DEFAULT_INSTANCE);

    ble.init(onBluetoothInitialized);

    // wait for Bluetooth Radio to be initialized

    while (ble.hasInitialized() == false);

    while (1) {

        // put radio to sleep in between broadcasts

        ble.waitForEvent();
    }

}
```

```
void blinkHeartbeat(void) {

    /* Do blinky on LED1 to indicate system aliveness. */
```

