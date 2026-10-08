
## Chapter 15. C on Arduino

To use digital output, you first need to configure the pin as an OUTPUT using the pinMode() function. For example:

```
pinMode(13, OUTPUT); // Set pin 13 as output
digitalWrite(13, HIGH); // Turn pin 13 on (5V)
digitalWrite(13, LOW); // Turn pin 13 off (0V)
```

Digital output are commonly used to control:

- LEDs: Control visual indicators
- Relays: Switch high-power devices like motors or lights
- Buzzer/Speakers: Generate simple tones or sound effects
- Shift registers: Expand the number of digital outputs
- Transistors/MOSFETs: Drive higher-current devices

Some things to keep in mind:

- Don't overload the pins: Every Arduino board has a maximum current rating per pin (usually around 40mA). Overloading pins can lead to unreliable behavior or damage the Arduino. Refer to the board documentation for precise details.
- Higher currents: To control devices that draw more current than a single pin can provide (e.g., high-power LEDs, large motors), use transistors, MOSFETs, or drivers. These components amplify the Arduino's signal and handle higher currents effectively.
- Inductive Loads: Devices like motors or solenoids not only require higher current but also generate EMF (electromagnetic force) when switched off. Use flyback diodes (also known as freewheeling diodes) to absorb these voltage spikes.
- Analog Pins Can Be Too: In some Arduino boards, some analog input pins (like A0, A1, etc.) can also function as digital outputs.

## Digital Input

Digital input means whether a pin is at high voltage or low voltage. The high or low voltage is usually referenced against half of the supply voltage (Vcc) of the microcontroller. If the voltage of the pin is above Vcc/2, the pin is considered to be high.

The state of a pin is determined by using the digitalRead() function. The function accepts an argument, the number of pins to be read (0-13 or A0-A5), and returns the pin state as 1 (HIGH) or 0 (LOW).

The digital state of a pin can be whether or not it is set as an output. However, when you read the state of a pin that is set to output, you will only be reading the defined output state.

```
int pinState; // Declare variable to store pin state
pinState = digitalRead(2); // Reads the state of pin 2
```

## 15.3. Arduino vs Regular C

When a pin is set as input, its voltage depends on the connected circuit, not on the microcontroller. If the circuit is disconnected (e.g., by a switch), the pin's state becomes uncertain, known as floating. To prevent this uncertainty, a pull-up or pull-down resistor is connected to the input pin. This resistor connects the input pin to high voltage or ground, ensuring that when the switch is open, the pin is pulled to either HIGH or LOW.

## 15.3.3 Arduino Standard I/O Library

In Arduino, you can use standard input/(I/O) functions to communicate through the serial port on the PC. The Arduino IDE provides a built-in Serial Monitor for sending and receiving data from the board. You can also use terminal emulator applications like PuTTY on the PC to communicate with the Arduino board.

The main functions for standard I/O are:

- `Serial.begin(baud,rate)`: This function initializes the serial communication at the specified baud rate. For example, Serial.begin(9600); sets the baud rate to 9600 bits per second.
- `Serial.print(data)`: This function sends the specified data to the serial port. The data can be a number, a string, or any other data type that can be converted to a string.
- `Serial.print(x, 3); // Print float x with 3 significant digits
- `Serial.println(data)`: This function is similar to Serial.print(), but it also adds a newline character ('\n') at the end of the output.
- `Serial.available()`: This function returns the number of bytes (characters) available to read from the serial port.
- `Serial.read()`: This function reads a single byte (character) from the serial port. If no data are available, it returns -1.
- `Serial.readBytes(buffer, length)`: This function reads up 'length' bytes from the serial port and stores them in the provided 'buffer' array.
- `Serial.readBytesUntil(terminator, buffer, length)`: This function reads from the serial port until it encounters the specified 'terminator' character, or until it has read 'length' bytes. Bytes are stored in the 'buffer' array.

![](img/33fb6b7acbb6df48a3c9564e97117da6_246_0.png)

## Chapter 15. C on Arduino

Here is an example of how to use these functions:

```
// Arduino code
void setup() {
  Serial.begin(9600); // Initialize serial communication at 9600 baud
}

void loop() {
  if (Serial.available() > 0) { // Check if there is data available
  char input = Serial.read(); // Read a single byte from the serial port
  Serial.print("You entered: ");
  Serial.println(input); // Print the input character with a newline
  }
}
```

Then, on the Arduino IDE Serial Monitor, you can type characters in the input field and... (Wait, the text ends here).

Actually, looking at the provided OCR, the text ends abruptly. Let me re-process based on the provided blocks.

Wait, I see the text provided in the prompt is a mix of pages. I will merge them logically.

(Self-correction: The OCR text provided in the prompt contains multiple versions of some sections or overlapping content. I will follow the order provided but clean up the broken formatting.)

Actually, looking closely at the OCR provided:
Page 245: Chapter 15 intro, Digital output, Digital Input.
Page 246: 15.3 Arduino vs Regular C, 15.3.3 Arduino Standard I/O Library.
Page 247: Chapter 15 C on Arduino (repeated header), example code.
Page 248: 15.3 Arduino vs Regular C (repeated header), String Object, String Methods.

It seems the OCR has some duplicates or is a compilation. I will provide the clean version of the content flow provided.

[content]
## Chapter 15. C on Arduino

To use digital output, you first need to configure the pin as an OUTPUT using the pinMode() function. For example:

```
pinMode(13, OUTPUT); // Set pin 13 as output
digitalWrite(13, HIGH); // Turn pin 13 on (5V)
digitalWrite(13, LOW); // Turn pin 13 off (0V)
```

Digital output are commonly used to control:

- LEDs: Control visual indicators
- Relays: Switch high-power devices like motors or lights
- Buzzer/Speakers: Generate simple tones or sound effects
- Shift registers: Expand the number of digital outputs
- Transistors/MOSFETs: Drive higher-current devices

Some things to keep in mind:

- Don't overload the pins: Every Arduino board has a maximum current rating per pin (usually around 40mA). Overloading pins can lead to unreliable behavior or damage the Arduino. Refer to the board documentation for precise details.
- Higher currents: To control devices that draw more current than a single pin can provide (e.g., high-power LEDs, large motors), use transistors, MOSFETs, or drivers. These components amplify the Arduino's signal and handle higher currents effectively.
- Inductive Loads: Devices like motors or solenoids not only require higher current but also generate EMF (electromagnetic force) when switched off. Use flyback diodes (also known as freewheeling diodes) to absorb these voltage spikes.
- Analog Pins Can Be Too: In some Arduino boards, some analog input pins (like A0, A1, etc.) can also function as digital outputs.

## Digital Input

Digital input means whether a pin is at high voltage or low voltage. The high or low voltage is usually referenced against half of the supply voltage (Vcc) of the microcontroller. If the voltage of the pin is above Vcc/2, the pin is considered to be high.

The state of a pin is determined by using the digitalRead() function. The function accepts an argument, the number of pins to be read (0-13 or A0-A5), and returns the pin state as 1 (HIGH) or 0 (LOW).

The digital state of a pin can be whether or not it is set as an output. However, when you read the state of a pin that is set to output, you will only be reading the defined output state.

```
int pinState; // Declare variable to store pin state
pinState = digitalRead(2); // Reads the state of pin 2
```

## 15.3. Arduino vs Regular C

When a pin is set as input, its voltage depends on the connected circuit, not on the microcontroller. If the circuit is disconnected (e.g., by a switch), the pin's state becomes uncertain, known as floating. To prevent this uncertainty, a pull-up or pull-down resistor is connected to the input pin. This resistor connects the input pin to high voltage or ground, ensuring that when the switch is open, the pin is pulled to either HIGH or LOW.

## 15.3.3 Arduino Standard I/O Library

In Arduino, you can use standard input/(I/O) functions to communicate through the serial port on the PC. The Arduino IDE provides a built-in Serial Monitor for sending and receiving data from the board. You can also use terminal emulator applications like PuTTY on the PC to communicate with the Arduino board.

The main functions for standard I/O are:

- `Serial.begin(baud,rate)`: This function initializes the serial communication at the specified baud rate. For example, Serial.begin(9600); sets the baud rate to 9600 bits per second.
- `Serial.print(data)`: This function sends the specified data to the serial port. The data can be a number, a string, or any other data type that can be converted to a string.
- `Serial.print(x, 3); // Print float x with 3 significant digits
- `Serial.println(data)`: This function is similar to Serial.print(), but it also adds a newline character ('\n') at the end of the output.
- `Serial.available()`: This function returns the number of bytes (characters) available to read from the serial port.
- `Serial.read()`: This function reads a single byte (character) from the serial port. If no data are available, it returns -1.
- `Serial.readBytes(buffer, length)`: This function reads up 'length' bytes from the serial port and stores them in the provided 'buffer' array.
- `Serial.readBytesUntil(terminator, buffer, length)`: This function reads from the serial port until it encounters the specified 'terminator' character, or until it has read 'length' bytes. Bytes are stored in the 'buffer' array.

![](img/33fb6b7acbb6df48a3c9564e97117da6_246_0.png)

## Chapter 15. C on Arduino

Here is an example of how to use these functions:

```
// Arduino code
void setup() {
  Serial.begin(9600); // Initialize serial communication at 9600 baud
}

void loop() {
  if (Serial.available() > 0) { // Check if there is data available
  char input = Serial.read(); // Read a single byte from the serial port
  Serial.print("You entered: ");
  Serial.println(input); // Print the input character with a newline
  }
}
```

## 15.3. Arduino vs Regular C
(Wait, the OCR text repeats here on page 248. I will include the unique content from page 248.)

## String Object

Constructing a string object has the following syntax:

```
String(val)
String(val, base)
String(val, decimalPlaces)
```

where

- val: a variable to format as a String. Allowed data types: string, char, byte, int, long, unsigned int, unsigned long, float, double
- base: (optional) the base in which to format an integral value.
- decimalPlaces: only if val is float or double.

Here are some examples of how to declare and use String in Arduino:

```
// using a constant String
stringOne = "Hello String";
// converting a constant string into a String object
stringTwo = String("This is a string");
// concatenating two strings
StringThree = String(stringTwo + " with more");
// using a constant integer
StringFour = String(13);
// using an int and a base
stringFive = String(analogRead(0), DEC);
// using an int and a base (hexadecimal)
stringSix = String(45, HEX);
// using an int and a base (binary)
stringSeven = String(255, BIN);
// using a long and a base
stringEight = String(millis(), DEC);
// using a float and the decimal places
stringNine = String(5.698, 3);
```

## 15.3.4 Arduino String Type

The String data type is object-oriented. Here are a few reasons why you might choose String:

- **String methods**: The String type provides built-in methods that simplify string operations.
- **Variable Length Strings**: Unlike character arrays, Strings can change in length.
- **Compatibility with Libraries**: Many Arduino libraries accept and return String objects.

However, it is important to note that the String data type uses dynamic allocation, which can lead to memory fragmentation, especially on boards with limited RAM.

## String Methods

In Arduino programming, they may seem similar, there are some key differences. Functions are standalone pieces of code that perform specific tasks. They have their own scope and can only access their own variables. Methods, on the other hand, are associated with objects or instances of a class. They can access and interact with the data and state of the object they belong to. Other differences:

Scope: Functions have their own scope and can only access their own variables. Methods can access the data of the object they belong to.
