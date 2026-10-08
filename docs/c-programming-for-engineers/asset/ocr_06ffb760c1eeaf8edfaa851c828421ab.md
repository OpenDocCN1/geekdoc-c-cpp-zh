# Chapter 15. C on Arduino

Invocation Functions are called by their name and any required parameters.
Methods use the dot notation on an object instance.

Return value : Functions can return values, but methods usually modify the object's state rather than directly returning values.

To find the length of a string you can use either the strlen() function or the length() method. The function works independently, while the method is associated with the String object and can directly access its internal data. Here is an example of Arduino code that demonstrates this functionality.

```
#include <Arduino.h>
#include <String.h>
#include <string.h>

void setup() {
  Serial.begin(9600);

  char cString[] = "Hello, World!";
  String arduinoString = "Hello, World!";

  // Using strlen() function
  int length = strlen(cString);
  Serial.print("String length: ");
  Serial.println(length);

  // Using the String length() method
  length = arduinoString.length();
  Serial.print("String length: ");
  Serial.println(length);
}
```

```
void loop() {
  // Nothing to do in the loop
}
```

The <Arduino.h> header provides core Arduino functionality. The <String.h> header file provides the Arduino String class for manipulating strings. Lastly, the <string.h> header file provides the C standard library string functions. Both the strlen() function in C/C++ and the length() method in the Arduino String object serve the same purpose of determining the length of a string.

# 15.4 Hello World in Arduino

"Hello, World!" program has become a tradition and part of programming culture. It is often the first program that programmers write in a new language. In this section, we will write the "Hello, World!" in Arduino C.

In Arduino, a sketch refers to the code written for an Arduino board. A sketch is typically written using the Arduino Integrated Development Environment (IDE)