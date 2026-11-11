by default; floats will print to two decimal places by default, and so forth.

You can send characters or strings as is to the print statement and it will print them without any issue.

```
Serial.println(value, OPTIONAL format)
```

This will allow you to print out values just like you would with the normal print method

```
Serial.read()
```

This will read in the data which is coming in through the serial port. Simple enough! It is added to an incoming stream of serial data called the serial buffer. When you read from this buffer, the information is destroyed, so be sure to save the data to a variable if you need to reuse it at some point.

```
Serial.readBytes(serialBuffer, numberOfBytes)
```

This will read in characters from the serial port to a buffer. You can determine the number of bytes that are to be read. Your buffer must be either a char array or a byte array.

```
Serial.readBytesUntil(terminatorCharacter, serialBuffer, numberOfBytes)
```

This will read in characters from the serial either until the given number of bytes has been read or until a given terminating character has been read. In either case, the method will terminate.

```
Serial.write()
```

This will write data to the serial port; however, this particular method only sends binary data to the serial port. If you need to send ASCII data, you should use the print method instead.

```
Serial.serialEvent()
```

Whenever data comes to be available for use by the serial port, this function will be called. You can then use the Serial.read() function in order to read in data from the serial port.