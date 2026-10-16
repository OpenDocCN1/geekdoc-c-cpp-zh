Such a documentation file serves a secondary purpose as an annotated copy of the header file in that it serves as a *backup* for the header file.

# 6.4.2 Using a Library in a Program

Once our library Heat has been constructed, we can use it in a program like that in Example 6.10 for solving a temperature-conversion problem.

```
### Example 6.10 Converting a Temperature Using a Library

```cpp
/* This program converts temperatures from Celsius to Fahrenheit, using
   function fahrenheitToCelsius() that is stored in library Heat.

   Input:  tempFahrenheit
   Output: tempCelsius
---------------------------------------------------------------*/

#include <iostream>              //cin, cout, <<, >>
using namespace std;
#include "Heat.h"                 // our library's header file

int main()
{
   cout << "Program to convert Celsius temperatures to Fahrenheit.\n";

   double tempCelsius,        // Celsius temperature
          tempFahrenheit;      // Fahrenheit temperature

   cout << "\nEnter a Celsius temperature (< -273.15 to stop): ";
   cin >> tempCelsius;
   while (tempCelsius >= -273.15)
   {
      tempFahrenheit = 1.8 * tempCelsius + 32;

      cout << tempCelsius << " degrees Celsius is equivalent to "
           << tempFahrenheit << " degrees Fahrenheit\n";
      cout << "\nEnter a Celsius temperature (< -273.15 to stop): ";
      cin >> tempCelsius;
   }
}
```
```

Execution of this program is identical to that in Example 6.2. In this program, however, the prototype of `celsiusToFahrenheit()` before the main function has been replaced by the line

```
```cpp
#include "Heat.h"
```
```