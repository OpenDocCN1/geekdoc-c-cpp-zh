```
array<wchar_t^> indicators = gcnew array<wchar_t>(sentence->Length){L' '};

int index = 0;                     // Index of character found
int count = 0;                    // Count of punctuation characters
while((index = sentence->IndexOfAny(punctuation, index)) >= 0)
{
    indicators[index] = L'^';      // Set marker
    ++index;                      // Increment to next character
    ++count;                      // Increase the count
}
Console::WriteLine(L"There are {0} punctuation characters in the string:", count);
Console::WriteLine(L"\n{0}\n{1}", sentence, gcnew String(indicators));
return 0;
}
```

This example should produce the following output:

```
There are 6 punctuation characters in the string:

"It's chilly in here", the boy's mother said coldly.
^  ^      ^^     ^
Press any key to continue . . .
```

# How It Works

You first create an array containing the characters to be found and the string to be searched:

```
array<wchar_t^> punctuation = {L'"', L'\'', L'.', L',', L':', L';', L'!', L'?' };
String^ sentence = L"\"It's chilly in here\", the boy's mother said coldly.";
```

Note that you must specify a single quote character using an escape sequence because a single quote is a delimiter in a character literal. You can use a double quote explicitly in a character literal because there's no risk of it being interpreted as a delimiter in this context.

Next you define an array of characters with the elements initialized to a space character:

```
array<wchar_t^> indicators = gcnew array<wchar_t>(sentence->Length){L' '};
```

This array has as many elements as the sentence string has characters. You'll be using this array in the output to mark where punctuation characters occur in the sentence string. You'll just change the appropriate array element to '^' whenever a punctuation character is found. Note how a single initializer between the braces following the array specification can be used to initialize all the elements in the array.

The search takes place in the while loop:

```
while((index = sentence->IndexOfAny(punctuation, index)) >= 0)
{
    indicators[index] = L'^';      // Set marker
    ++index;                      // Increment to next character
    ++count;                      // Increase the count
}
```