80

Chapter 5. Operators

# Table 5.6: Fixed-size integer data types

| Data Type | Range |
|--- | --- |
| uint8_t | 0 to 255 |
| int8_t | -128 to 127 |
| uint16_t | 0 to 65,535 |
| int16_t | -32,768 to 32,767 |
| uint32_t | 0 to 4,294,967,295 |
| int32_t | -2,147,483,648 to 2,147,483,647 |
| uint64_t | 0 to 18,446,744,073,709,551,615 |
| int64_t | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |

A common practice in embedded systems programming is to use fixed-size integer data types (uint8_t, uint32_t, etc) from the <stddef.h> library. See Table 5.6 for the complete list. These data types offer several benefits:

+   **Predictability**: Fixed-size types ensure consistent behavior across different platforms. For example, uint8_t will always be an 8-bit unsigned integer, regardless of the system, which will prevent bugs.
* **Memory Efficiency**: By knowing the value a variable will hold, you can choose the smallest data type capable of handling those values. This can save memory, especially in systems with limited resources where every byte counts.
* **Portability**: Standard integer types like int or long can vary in size between different systems or compilers. By using fixed-size integers, you ensure that your code behaves the same way on all platforms.
* **Safety**: Fixed-size types help avoid overflows, underflows, and unintended conversions that can occur with standard integer types.

To use fixed-size integers in C, include the <stddef.h> header file. Here's an example program demonstrating their use:

```
#include <stddef.h>
#include <stdio.h>

int main() {
    // Fixed-size integer declarations
    int8_t myInt8 = -10;
    uint8_t myUint8 = 255;
    uint16_t myUint16 = 50000;
    int32_t myInt32 = -10000000;
    uint64_t myUint64 = 12345678901234566;

    // Increment my_var
    myUint8++;

    // Printing the values
    printf("int8_t: %d\n", myInt8);
```

![](bbox=[0.055, 0.935, 0.132, 0.986])