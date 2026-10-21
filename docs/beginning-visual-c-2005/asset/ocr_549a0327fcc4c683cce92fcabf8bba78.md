Let’s put this in a working example that demonstrates how you can process arrays of arrays.

# Try It Out   Using an Array of Arrays

Create a CLR console program project and modify it as follows:

```
// Ex4_16.cpp : main project file.
// Using an array of arrays

#include "stdafx.h"

using namespace System;

int main(array<System::String ^> ^args)
{
array< array< String^ >^ > grades = gcnew array< array< String^ >^ >
{
    gcnew array<String^>{"Louise", "Jack"},                 // Grade A
    gcnew array<String^>{"Bill", "Mary", "Ben", "Joan"},   // Grade B
    gcnew array<String^>{"Jill", "Will", "Phil"},          // Grade C
    gcnew array<String^>{"Ned", "Fred", "Ted", "Jed", "Ed"}, // Grade D
    gcnew array<String^>{"Dan", "Ann"}                      // Grade E
};

wchar_t gradeLetter = 'A';

for each(array< String^ >^ grade in grades)
{
    Console::WriteLine("Students with Grade {0}:", gradeLetter++);

    for each( String^ student in grade)
        Console::Write("{0,12}",student);                  // Output the current name

    Console::WriteLine();                                   // Write a newline
}
return 0;
}
```

This example produces the following output:

```
Students with Grade A:
    Louise          Jack
Students with Grade B:
    Bill            Mary            Ben             Joan
Students with Grade C:
    Jill            Will            Phil
Students with Grade D:
    Ned             Fred            Ted             Jed             Ed
Students with Grade E:
    Dan             Ann
Press any key to continue . . .
```