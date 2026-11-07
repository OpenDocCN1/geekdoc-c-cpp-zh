```
```cpp
int main(array<System::String ^> ^args)
{
    string sentence;
    char ltr;
    int numVowels = 0;
    cout << "Enter a sentence: ";
    getline(cin, sentence);
    for(int i = 0; i < sentence.size(); ++i)
    {
        ltr = sentence[i];
        if (isVowel(ltr))
            ++numVowels;
    }
    cout << "There are " << numVowels
         << " vowels in the sentence.";
    Console::ReadKey();
    return 0;
}
```
```

If we enter the following sentence:

Now is the time for all good people to come to the aid of their party

the output is:

There are 23 vowels in the sentence.

We perform one very interesting trick in this program. We loop through the sentence variable like it is an array. We can do that because, to C++, a string is an array. Internally, C++ stores a string as an array of char values. Knowing this allowed us to easily loop through the string, pulling each character out by using its index position in the “string” array and determining if the letter is a vowel or a consonant. We'll look more at treating strings as arrays when we talk about pointers later in the book.

The switch statement cannot be a universal replacement for the if statement due to the requirement that the condition being tested must be an integral expression. However, for those situations where it is