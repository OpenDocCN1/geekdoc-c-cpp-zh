# Try It Out Using a for each Loop to Access the Characters in a String

Create a new CLR console program project with the name Ex3_17 and modify the code to the following:

```
// Ex3_17.cpp : main project file.
// Analyzing a string using a for each loop

#include "stdafx.h"

using namespace System;

int main(array<System::String ^> ^args)
{
    int vowels = 0;
    int consonants = 0;
    String^ proverb = L"A nod is as good as a wink to a blind horse.";
    for each(wchar_t ch in proverb)
    {
        if(Char::IsLetter(ch))
        {
            ch = Char::ToLower(ch);      // Convert to lowercase
            switch(ch)
            {
            case 'a': case 'e': case 'i':
            case 'o': case 'u':
                ++vowels;
                break;
            default:
                ++consonants;
                break;
            }
        }
    }
    Console::WriteLine(proverb);
    Console::WriteLine(L"The proverb contains {0} vowels and {1} consonants.", vowels, consonants);

    return 0;
}
```

This example produces the following output.

```
A nod is as good as a wink to a blind horse.
The proverb contains 14 vowels and 18 consonants.
```

# How It Works

The program counts the number of vowels and consonants in the string referenced by the proverb variable. The program does this by iterating over each character in the string using a for each loop. You first define two variables used to accumulate the total number of vowels and the total number of consonants.

```
int vowels = 0;
int consonants = 0;
```