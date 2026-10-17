
```cpp
static const uint16_t serialNumberCharacteristicUuid = 0x2a04;

// Battery Level Characteristic UUID
static const uint16_t batteryLevelCharacteristicUuid = 0x2a19;

// model and serial numbers
static const char* modelNumber = "1AB2";
static const char* serialNumber = "1234";

int batteryLevel = 100;

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
 * Callback handler when a Central has disconnected
 *
 * @param[in] params Information about the connection
 */
void onCentralDisconnected(
    const Gap::DisconnectionCallbackParams_t *params
);

/** Build Service and Characteristic Relationships */
// Create a read/write/notify Characteristic
static uint8_t deviceNameCharacteristicValue[characteristicLength] = \
    BROADCAST_NAME;

ReadOnlyArrayGattCharacteristic<uint8_t, sizeof(characteristicValue)> \
    deviceNameCharacteristic(
        deviceNameCharacteristicUuid,
        characteristicValue);

static uint8_t modelNumberCharacteristicValue[characteristicLength] = \
    modelNumber;

ReadOnlyArrayGattCharacteristic<uint8_t, sizeof(characteristicValue)> \
    modelNumberCharacteristic(
        modelNumberCharacteristicUuid,
        characteristicValue);

static uint8_t serialNumberCharacteristicValue[characteristicLength] = \
    serialNumber;

ReadOnlyArrayGattCharacteristic<uint8_t, sizeof(characteristicValue)> \
characteristicValue,
GattCharacteristic::BLE_GATT_CHAR_PROPERTIES_READ | \
GattCharacteristic::BLE_GATT_CHAR_PROPERTIES_NOTIFY
);

GattCharacteristic *batteryLevelCharacteristics[] = {
  &batteryLevelCharacteristic
}

GattService batteryLevelService(
  batteryLevelServiceUuid,
  batteryLevelCharacteristics,
  sizeof(batteryLevelCharacteristics) / sizeof(GattCharacteristic *)
);

/**
 * Main program and loop
 */
int main(void) {
  serial.baud(9600);
  serial.printf("Starting Peripheral\\r\\n");
  ticker.attach(blinkHeartbeat, 1); // Blink status led every 1 second
  // initialized Bluetooth Radio

BLE &ble = BLE::Instance(BLE::DEFAULT_INSTANCE);
ble.init(onBluetoothInitialized);
// wait for Bluetooth Radio to be initialized
while (ble.hasInitialized() == false);

while (1) {
    // save power when possible
    ble.waitForEvent();
}

}

void blinkHeartbeat(void) {
/* Do blinky on LED1 to indicate system aliveness. */
statusLed = !statusLed;
}

void onBluetoothInitialized(
    BLE::InitializationCompleteCallbackContext *params)
{
BLE&   ble = params->ble;
ble_error_t error = params->error;

// quit if there's a problem
if(error != BLE_ERROR_NONE) {
    return;
}
// Ensure that it is the default instance of BLE
if(ble.getInstanceID() != BLE::DEFAULT_INSTANCE) {
    return;
}

serial.printf("Describing Peripheral...");
// attach Services
ble.addService(customService);
// process disconnections with a callback
ble.gap().onDisconnection(onCentralDisconnected);
// advertising parameters
ble.gap().accumulateAdvertisingPayload(
    // Device is Peripheral only
    GapAdvertisingData::BREDR_NOT_SUPPORTED |
    // always discoverable
    GapAdvertisingData::LE_GENERAL_DISCOVERABLE);
// broadcast name
ble.gap().accumulateAdvertisingPayload(
    GapAdvertisingData::COMPLETE_LOCAL_NAME,
    (uint8_t *)BROADCAST_NAME, sizeof(BROADCAST_NAME)
);
// advertise services
ble.gap().accumulateAdvertisingPayload(
    GapAdvertisingData::COMPLETE_LIST_16BIT_SERVICE_IDS,
    (uint8_t *)uuid16_list, sizeof(uuid16_list)
);
// allow connections
ble.gap().setAdvertisingType(
    GapAdvertisingParams::ADV_CONNECTABLE_UNDIRECTED);
// advertise every 1000ms
ble.gap().setAdvertisingInterval(1000); // 1000ms
// set the GATT values
ble.gattServer().write(
    deviceNameCharacteristic.getValueHandle(),
    BROADCAST_NAME,
    characteristicLength
);
ble.gattServer().write(
    modelNumberCharacteristic.getValueHandle(),
    modelNumber,
    characteristicLength
);
ble.gattServer().write(
    serialNumber.getValueHandle(),
    serialNumber,
    characteristicLength
);
ble.gattServer().write(
    batteryLevelCharacteristic.getValueHandle(),
    batteryLevel,
    characteristicLength
);
// begin advertising
ble.gap().startAdvertising();
serial.printf(" done\r\n");
}

void onCentralDisconnected(const Gap::DisconnectionCallbackParams_t *params)
{
    BLE::Instance().gap().startAdvertising();
    serial.printf("Central disconnected\r\n");
}
```

运行时，这个草图会创建一个以“MyDevice”为广播名称的外设（Peripheral），并提供一个 GATT 配置文件（profile），其中包含一个具有读写权限的特性（Characteristic）（图 6-2）。

- 设备信息服务：`000180a-000-1000-8000-00805f9-b34fb`
- 设备名称特性：`0002a00-000-1000-8000-00805f9-b34fb`
- 型号特性：`0002a24-000-1000-8000-00805f9-b34fb`
- 序列号特性：`0002a04-000-1000-8000-00805f9-b34fb`
- 设备信息服务：`000180a-000-1000-8000-00805f9-b34fb`
- 电池电量服务：`000180f-000-1000-8000-00805f9-b34fb`
- 电池电量特性：`0002a19-000-1000-8000-00805f9-b34fb`
- 服务：`000180c-000-1000-8000-00805f9-b34fb`
- 特性：`0002a56-000-1000-8000-00805f9-b34fb`

图 6-2：nRF 上承载的 GATT 配置文件

## 示例代码

本章的示例代码可在以下网址获取：https://github.com/BluetoothLowEnergyInCppWithnRFx/Chapter06

## 从外设读取数据

低功耗蓝牙（Bluetooth Low Energy）的真正价值在于其无线传输数据的能力。

蓝牙外设（Peripheral）是被动设备，因此它们不会向已连接的中心设备（Central）推送数据。相反，中心设备会请求从某个特性（Characteristic）读取数据。只有在特性启用了读取属性（Read Attribute）时，读取才能发生。

这被称为“从特性读取值”。

因此，如果外设更改了某个特性的值，随后中心设备从外设下载数据时，过程如图 7-1 所示：

![](img/d7b9d81704fe6839dbdc99a45736bfb5_85_0.png)

**外设**

![](img/d7b9d81704fe6839dbdc99a45736bfb5_85_1.png)

**中心设备**

![](img/d7b9d81704fe6839dbdc99a45736bfb5_85_2.png)

设置特征值

读取数据

响应数据

图 7-1. 中心设备从外设读取数据的过程

中心设备可以重复读取特征值，无论该特征值的值是否已发生变化。

### 外设编程

通过 BLE 传输数据相当容易。这要求外设拥有一个中心设备可读取的特征值。

创建一个服务和一个具有读取属性、最长 20 字节的特征值。例如，一个 16 字节的只读特征值：

```cpp
// create a 16-byte long Characteristic value, initialize with zeroes
static uint8_t characteristicValue[16] = {0};

// create a Read only Characteristic
ReadOnlyArrayGattCharacteristic<uint8_t, sizeof(characteristicValue)> \
characteristic(
"2A56", // UUID 2a56
characteristicValue // use the Characteristic value
);
```

每个服务和特征值都必须能够通过 UUID 唯一标识。

这样，特征值中的数据就可以在本地设置，以便已连接的中心设备从中读取。

```cpp
char* outputString = "Hello World";
int stringLength = 12;

ble.gattServer().write(
    characteristic.getValueHandle(),
    outputString,
    stringLength
);
```

### 整合全部内容

创建一个名为 `ble_send_data` 的新草图，然后将以下代码复制到该草图中。

该草图每 5 秒将特征值设置为一个随机字符串。

#### 示例 7–1. `ble_send_data/main.c`

```cpp
#include "mbed.h"
#include "ble/BLE.h"

/** User interface I/O */

// instantiate USB Serial
Serial serial(USBTX, USBRX);
// Status LED
DigitalOut statusLed(LED1, 0);
// Timer for blinking the statusLed
Ticker ticker;

/** Bluetooth Peripheral Properties **/

// Broadcast name
const static char BROADCAST_NAME[] = "MyDevice";
// Service UUID
static const uint16_t customServiceUuid = 0x180C;
// array of all Service UUIDs
static const uint16_t uuid16_list[] = { customServiceUuid };
// Number of bytes in Characteristic
static const uint8_t characteristicLength = 20;
// Characteristic UUID
static const uint16_t characteristicUuid = 0x2A56;

/** State **/

// Storage for written Characteristic value
char bleCharacteristicValue[characteristicLength];
uint16_t bleCharacteristicValueLength = 0;

/** Functions **/

/**
* create a random string
*/
static const char alphanum[] = "0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ";

void writeRandomStringToCharacteristic();

/**
* Callback triggered when the ble initialization process has finished
*
* @param[in] params Information about the initialized Peripheral
*/
void onBluetoothInitialized(
    BLE::InitializationCompleteCallbackContext *params
);

/**
```
