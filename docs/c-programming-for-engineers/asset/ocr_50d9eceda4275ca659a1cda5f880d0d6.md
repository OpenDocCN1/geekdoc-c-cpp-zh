# 15.3. Arduino vs Regular C

When a pin is set as input, its voltage depends on the connected circuit, not on the microcontroller. If the circuit is disconnected (e.g., by a switch), the pin's state becomes uncertain, known as floating. To prevent this uncertainty, a pull-up or pull-down resistor is connected to the input pin. This resistor connects the input pin to high voltage or ground, ensuring that when the switch is open, the pin is pulled to either HIGH or LOW.

# 15.3.3 Arduino Standard I/O Library

In Arduino, you can use standard input/(I/O) functions to communicate through the serial port on the PC. The Arduino IDE provides a built-in Serial Monitor for sending and receiving data/from the board. You can also use terminal emulator applications like PuTTY on the PC to communicate with the Arduino board.
The main functions for standard I/O are:

+   * Serial.begin(baud,rate): This function initializes the serial communication at the specified baud rate. For example, Serial.begin(9600); sets the baud rate to 9600 bits per second.
* Serial.print(data): This function sends the specified data to the serial port. The data can be a number, a string, or any other data type that can be converted to a string.
* Serial.print(x, 3); // Print float x with 3 significant digits
* Serial.println(data): This function is similar to Serial.print(), but it also adds a newline character ('
') at the end of the output.
* Serial.available(): This function returns the number of bytes (characters) available to read from the serial port.
* Serial.read(): This function reads a single byte (character) from the serial port. If no data are available, it returns -1.
* Serial.readBytes(buffer, length): This function reads up 'length' bytes from the serial port and stores them in the provided 'buffer' array.
* Serial.readBytesUntil(terminator, buffer, length): This function reads from the serial port until it encounters the specified 'terminator' character, or until it has read 'length' bytes. Bytes are stored in the 'buffer' array.

![](bbox=[0.048, 0.735, 0.953, 0.988])