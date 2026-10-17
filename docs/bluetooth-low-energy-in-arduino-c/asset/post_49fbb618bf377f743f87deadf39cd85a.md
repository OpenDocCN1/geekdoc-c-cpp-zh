
- **Central** - A Bluetooth Low Energy device that can connect to several Peripherals.

- **Channel** - A finely-tuned radio frequency used for Broadcasting or data transmission.

- **Characteristic** - A port or data endpoint where data can be read or written.

- **Descriptor** - A feature of a Characteristic that allows for some sort of data interaction, such as Read, Write, or Notify.

- **E0** - The encryption algorithm built into Bluetooth Low Energy.

- **Generic Attribute (GATT) Profile** - A list of Services and Characteristics which are unique to a Peripheral and describe how data is served from the Peripheral. GATT profiles are hosted by a Peripheral.

- **iBeacon** - An Apple compatible Beacon which allows a Central to download a specific packet of data to inform the Central of its absolute location and other properties.

- **Intel® Curie™ Module** - The Intel® module that powers the Arduino 101 and contains the Bluetooth chipset.

- **Notify** - An operation where a Peripheral alerts a Central of a change in data.

- **Peripheral** - A Bluetooth Low Energy device that can connect to a single Central. Peripherals host a Generic Attribute (GATT) profile.

- **Read** - An operation where a Central downloads data from a Characteristic.

- **Scan** - The process of a Central searching for Broadcasting Peripherals.

- **Scan Response** - A feature of Bluetooth Low Energy which allows Centrals to download a small packet of data without connecting.

- **Service** - A container structure used to organize data endpoints. Services are hosted by a Peripheral.

- **Universally Unique Identifier (UUID)** - A long, randomly generated alphanumeric string that is unique regardless of where it’s used. UUIDs are designed to avoid name collisions that may happen when countless programs are interacting with each other.

- **Write** - An operation where a Central alters data on a Characteristic.

## About the Author

![](img/d7b9d81704fe6839dbdc99a45736bfb5_219_0.png)

Tony’s infinite curiosity compels him to want to open up and learn about everything he touches, and his excitement compels him to share what he learns with others.

He has two true passions: branding and inventing.

His passion for branding led him to start a company that did branding and marketing in 4 countries for firms such as Apple, Intel, and Sony BMG. He loves weaving the elements of design, writing, product, and strategy into an essential truth that defines a company.

His passion for inventing led him to start a company that uses brain imaging to quantify meditation and to predict seizures, a company acquired $1.5m in funding and was incubated in San Francisco where he currently resides.

Those same passions have led him on some adventures as well, including living in a Greek monastery with orthodox monks and to tagging along with a gypsy in Spain to learn to play flamenco guitar.

## About this Book

This book is a practical guide to programming Bluetooth Low Energy for Android phones and Tablets.

In this book, you will learn the basics of how to program an Android device to communicate with any Central or Peripheral device over Bluetooth Low Energy. Each chapter of the book builds on the previous one, culminating in three projects:

- A Beacon and Scanner
- An Echo Server and Client
- A Remote Controlled Device

Through the course of the book you will learn important concepts that relate to:

- How Bluetooth Low Energy works
- How data is sent and received
- Common paradigms for handling data

## Skill Level

This book is excellent for anyone who has basic or advanced knowledge of Java programming on Android.

## Other Books in this Series

If you are interested in programming other Bluetooth Low Energy Devices, please check out the other books in this series or visit [bluetoothlowenergybooks.com](http://bluetoothlowenergybooks.com):

![](img/d7b9d81704fe6839dbdc99a45736bfb5_223_0.png)

### Bluetooth Low Energy Programming in Android Java

Tony Gaitatzis, 2017

ISBN: 978-1-7751280-1-4

![](img/d7b9d81704fe6839dbdc99a45736bfb5_224_0.png)

### Bluetooth Low Energy Programming in iOS Swift

Tony Gaitatzis, 2017

ISBN: 978-1-7751280-0-7

![](img/d7b9d81704fe6839dbdc99a45736bfb5_224_1.png)

### Bluetooth Low Energy Programming in C++ for nRF Microcontrollers

Tony Gaitatzis, 2017

ISBN: 978-1-7751280-3-8

(this page intentionally left blank)

- **Advertise** - A feature of Bluetooth Low Energy where a Peripheral outputs a name and other specific data about itself.

- **Attribute** - A unit of a GATT Profile which can be accessed by a Central, such as a Service or a Characteristic.

- **Beacon** - A Bluetooth Low Energy Peripheral which continually Advertises so that Centrals can discern their location from information gleaned from the properties of the advertisement.

- **Big-endian** - A mechanism for storing numbers in binary, where the most significant value of the number is stored first, typically represented towards the right of the screen.

- **Bluetooth Low Energy (BLE)** - A low-power, short-range wireless protocol for use with microelectronics.

- **Central** - A Bluetooth Low Energy device that can connect to several Peripherals.

- **Channel** - A finely-tuned radio frequency used for Advertising or data transmission.

- **Characteristic** - A port or data endpoint where data can be read or written.

- **Descriptor** - A feature of a Characteristic that allows for some sort of data interaction, such as Read, Write, or Notify.

- **E0** - The encryption algorithm built into Bluetooth Low Energy.

- **Generic Access Profile (GAP)** - Identifying information about a Peripheral that identifies the Peripheral by name, service listing, connectability, or other custom data. This data is accessible after connection and is stored in big-endian format.

- **iBeacon** - An Apple-compatible Beacon which allows a Central to download a specific packet of data to inform the Central of its absolute location and other properties.

- **Little-Endian** - A mechanism for storing numbers in binary, where the least significant value of the number is stored first, typically represented towards the right of the screen.

- **Notify** - An operation where a Peripheral alerts a Central of a change in data.

- **Peripheral** - A Bluetooth Low Energy device that can connect to a single Central. Peripherals host a Generic Attribute (GATT) profile.

- **Read** - An operation where a Central downloads data from a Characteristic.

- **Scan** - The process of a Central searching for Advertising Peripherals.

- **Scan Response** - A feature of Bluetooth Low Energy which allows Centrals to download a small packet of data without connecting.

- **Service** - A container structure used to organize data endpoints. Services are hosted by a Peripheral.

- **Universally Unique Identifier (UUID)** - A long, randomly generated alphanumeric string that is unique regardless of where it’s used. UUIDs are designed to avoid name collisions that may happen when countless programs are interacting with each other.

- **Write** - An operation where a Central alters data on a Characteristic.

- **Android** - An open-source operating system used for smartphones and tablet computers.

- **Advertise** - A feature of Bluetooth Low Energy where a Peripheral outputs a name and other specific data about itself.

- **Beacon** - A Bluetooth Low Energy Peripheral which continually Advertises so that Centrals can discern their location from information gleaned from the properties of the advertisement.

- **Big-endian** - A mechanism for storing numbers in binary, where the most significant value of the number is stored first, typically represented towards the right of the screen.

- **Bluetooth Low Energy (BLE)** - A low-power, short-range wireless protocol for use with microelectronics.

- **Central** - A Bluetooth Low Energy device that can connect to several Peripherals.

- **Channel** - A finely-tuned radio frequency used for Advertising or data transmission.
