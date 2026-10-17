
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

/**
 * Main program and loop
 */

int main(void) {

    serial.baud(9600);

    serial.printf("Starting Peripheral\r\n");

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
```

```cpp
statusLed = !statusLed;

}

void onBluetoothInitialized(

    BLE::InitializationCompleteCallbackContext *params)

{

    BLE& ble = params->ble;

    BLE_error_t error = params->error;

    // quit if there's a problem

    if(error != BLE_ERROR_NONE) {

        return;

    }

    // Ensure that it is the default instance of BLE

    if(ble.getInstanceID() != BLE::DEFAULT_INSTANCE) {

        return;

    }

    serial.printf("Describing Peripheral...");

    // process disconnections with a callback

    ble.gap().onDisconnection(onCentralDisconnected);

    // advertising parametirs

ble.gap().accumulateAdvertisingPayload(

  // Device is Peripheral only

  GapAdvertisingData::BR_EDR_NOT_SUPPORTED |

  // always discoverable

  GapAdvertisingData::LE_GENERAL_DISCOVERABLE);

// broadcast name

ble.gap().accumulateAdvertisingPayload(

  GapAdvertisingData::COMPLETE_LOCAL_NAME,

  (uint8_t *)BROADCAST_NAME,

  sizeof(BROADCAST_NAME)

);

// allow connections

ble.gap().setAdvertisingType(

  GapAdvertisingParams::ADV_CONNECTABLE_UNDIRECTED

);

// advertise every 1000ms

ble.gap().setAdvertisingInterval(1000); // 1000ms

// begin advertising

ble.gap().startAdvertising();

serial.printf(" done\r\n");

}
```

```cpp
void onCentralDisconnected(const Gap::DisconnectionCallbackParams_t *params)
{
    BLE::Instance().gap().startAdvertising();
    serial.printf("Central disconnected\r\n");
}
```

当中心设备连接后，随后与外设断开时，串口监视器的输出应类似于下面这样（图5-3）。

```
Central connected: 45:b5:7d:96:01:2f

Central disconnected
```

## 图3-4 串口输出

您的外设现在可以处理连接和断开连接了。您可以修改回调函数，打开LED、向屏幕打印内容，或做其他任何事。

## 示例代码

本章代码可在以下网址获取：https://github.com/BluetoothLowEnergyInCppWithnRFx/Chapter05

## 服务与特征

在数据可以在中心设备与外设之间来回传输之前，外设必须托管一个GATT配置文件。也就是说，外设必须具备服务和特征。

## 识别服务与特征

每个服务和特征都由一个通用唯一标识符（UUID）来识别。UUID遵循格式0000XXXX-0000-1000-8000-00805f9b34fb，因此32位UUID 00002a56-0000-1000-8000-00805f9b34fb可以表示为0x2a56。

某些UUID预留用于特定用途。例如，任何16位UUID为0x2a35（或32位UUID 00002a35-0000-1000-8000-00805f9b34fb）的特征都被视为血压读数。

有关保留的服务UUID列表，请参阅*附录四：保留的GATT服务*。

有关保留的特征UUID列表，请参阅*附录五：保留的GATT特征*。

## 通用属性配置文件

服务和特征描述了外设上的一棵数据访问点树。这棵由服务和特征组成的树被称为通用属性（GATT）配置文件。把GATT想象成类似于文件夹和文件树可能会很有帮助（图6-1）。

![](img/d7b9d81704fe6839dbdc99a45736bfb5_64_0.png)

**图6-1 GATT配置文件的文件系统隐喻**

![](img/d7b9d81704fe6839dbdc99a45736bfb5_65_0.png)

**图6-2 GATT配置文件**

特征充当可进行通信的通道，服务则充当特征的容器。顶层服务称为主服务，位于另一个服务内部的服务称为次要服务。

特征的最大值长度为20字节，并且具有称为描述符的内部设置，这些描述符可以被修改。描述符使用UUID标识。一个稍后将会讨论的重要描述符是客户端特征配置（0x2902），它允许已连接的中心设备订阅该特征的变更通知。

有关保留描述符的列表，请参阅*附录五：GATT描述符*。

## 表6-1 特征权限

| 描述符 | 描述 |
|---|---|
| Read | 中心设备可以读取该特征，外设可以设置值。 |
| Write | 中心设备可以向该特征写入，当特征值改变时会通知外设，并且当写入操作发生时也会通知中心设备。 |
| Write without Response | 中心设备可以向该特征写入。当特征值改变时会通知外设，但中心设备不会收到写入操作已发生的通知。 |
| Notify | 当外设更改值时，中心设备会收到通知。 |

由于GATT配置文件托管在外设上，因此用来描述特征权限的术语是相对于外设如何访问该特征而言的。因此，当中心设备向外设上传数据时，外设可以从特征中“读取”。外设向特征“写入”新数据，并且可以“通知”中心设备数据已更改。

## 数据长度与速度

值得注意，低功耗蓝牙的最大数据包大小为20字节，速度为1 Mbit/s。

## 对外设进行编程

通用属性配置文件通过设置外设的服务和特征的UUID及权限来定义。

特征可以配置以下权限（表6-2）：

## 表6-2 BLE特征权限

| 值 |
|---|
| BLE_GATT_CHAR_PROPERTIES_READ |

![](img/d7b9d81704fe6839dbdc99a45736bfb5_68_0.png)

特征的最大长度为20字节。由于16位和8位数据类型在C++中易于传递，在示例中我们将使用`uint16_t`（无符号16位整数）和`uint8_t`（无符号8位整数）值。任何数据类型，包括自定义字节缓冲区，都可以通过BLE传输和组装。

定义一个UUID为`180c`（一个未注册的通用UUID）的服务：

```cpp
BLEService service("180C");
```

或者

```cpp
BLEService service("0000180C-000-1000-8000-00805f9-b34fb");
```

第一种方法让外设自动生成UUID的大部分，第二种方法则强制外设使用特定的UUID。第一种方法更简单但不够精确。第二种方法精确，并且适用于需要与外部人员或API共享UUID的项目。

某些UUID不可使用。如果选择了错误的UUID，外设可能会在没有警告的情况下崩溃。

nRF51822中提供了多种类型的特征，具体取决于你需要传输的数据类型。数组、整数、浮点数、布尔值和其他数据类型都有各自的特征构造函数。

例如，这个长度为2字节、UUID为`1801`的特征可以被中心设备读取，并且可以通知中心设备变更：

```cpp
static char readValue[2] = {0};
```

```cpp
ReadOnlyArrayGattCharacteristic
<uint8_t, sizeof(readValue)> readCharacteristic(
"1801",
(uint8_t *)readValue,
GattCharacteristic::BLE_GATT_CHAR_PROPERTIES_READ | \
GattCharacteristic::BLE_GATT_CHAR_PROPERTIES_NOTIFY
```

这个长度为8字节、UUID为`2A56`（数字特征）的特征可以被中心设备写入：

```cpp
static char writeValue[8] = {0};
```

```cpp
WriteOnlyArrayGattCharacteristic
<uint8_t, sizeof(writeValue)>writeCharacteristic(
writeCharacteristicUuid,
(uint8_t *)writeValue,
GattCharacteristic::BLE_GATT_CHAR_PROPERTIES_WRITE);
```

以下是可以创建的各种特定数据类型特征的示例：

```cpp
int properties = BLERead | BLEWrite | BLENotify;

ReadWriteBooleanCharacteristic booleanCharacteristic(
UUID,
properties,
maxLen
);

ReadWriteIntegerCharacteristic integerDataCharacteristicName(
UUID,
properties,
maxLen
);

BLEUnsignedIntCharacteristic yourCharacteristicName(
    UUID,
    properties,
    maxLen
);

BLELongCharacteristic yourCharacteristicName(
    UUID,
    properties,
    maxLen
);

BLEUnsignedLongCharacteristic yourCharacteristicName(
    UUID,
    properties,
    maxLen
);

BLEFloatCharacteristic yourCharacteristicName(UUID, properties, maxLen);
```

服务与特征通过`BLEPeripheral`添加到GATT配置文件中。将两个特征添加到服务之后，它们

它们被假定为同一个服务的一部分。这必须在 `blePeripheral.begin()` 之前发生。

```cpp
...
BLE &ble = BLE::Instance(BLE::DEFAULT_INSTANCE);
...
// Set up custom service
static const uint16_t customServiceUuid = 0x180C;
GattCharacteristic *characteristics[] = {
    &readCharacteristic, &writeCharacteristic
};
GattService customService(
    customServiceUuid,
    characteristics,
    sizeof(characteristics) / sizeof(GattCharacteristic *)
);
ble.addService(customService);
...
ble.gap().startAdvertising();
...
```

# 综合应用

创建一个名为 `ble_characteristics` 的新草图，并复制以下代码。

## 示例 6-1：`sketches/ble_characteristics/ble_characteristics.c`

```cpp
#include "mbed.h"

#include "ble/BLE.h"

/** User interface I/O **/

// instantiate USB Serial
Serial serial(USBTX, USBRX);

// Status LED
DigitalOut statusLed(LED1, 0);

// Timer for blinking the statusLed
Ticker ticker;

/** Bluetooth Peripheral Properties **/

// Broadcast name
const static char BROADCAST_NAME[] = "MyDevice";

// Device Information UUID

static const uint16_t deviceInformationServiceUuid = 0x180a;

// Battery Level UUID

static const uint16_t batteryLevelServiceUuid = 0x180f;

// array of all Service UUIDs

static const uint16_t uuid16_list[] = { customServiceUuid };

// Number of bytes in Characteristic

static const uint8_t characteristicLength = 20;

// Device Name Characteristic UUID

static const uint16_t deviceNameCharacteristicUuid = 0x2a00;

// Model Number Characteristic UUID

static const uint16_t modelNumberCharacteristicUuid = 0x2a24;

// Serial Number Characteristic UUID
```

