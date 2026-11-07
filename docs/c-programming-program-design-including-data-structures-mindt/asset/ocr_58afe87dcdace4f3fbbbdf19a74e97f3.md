```
```cpp
int main()                                      //Line 4
{                                               //Line 5
    string sentence = "Outside it is cloudy and warm.";  //Line 6
    string str = "cloudy";                      //Line 7

    string::size_type position;                 //Line 8

    cout << "Line 9: sentence = \"" << sentence
         << "\"" << endl;                       //Line 9

    cout << "Line 10: The position of \"is\" in sentence = "
         << static_cast<unsigned int> (sentence.find("is"))
         << endl;                                //Line 10

    cout << "Line 11: The position of 's' in sentence = "
         << static_cast<unsigned int> (sentence.find('s'))
         << endl;                                //Line 11

    cout << "Line 12: The position of \"" << str
         << "\" in sentence = "
         << static_cast<unsigned int> (sentence.find(str))
         << endl;                                //Line 12

    cout << "Line 13: The position of \"the\" in sentence = "
         << static_cast<unsigned int> (sentence.find("the"))
         << endl;                                //Line 13

    cout << "Line 14: The first occurrence of \'i\' in "
         << "sentence \n"
         << " after position 6 = "
         << static_cast<unsigned int> (sentence.find('i', 6))
         << endl;                                //Line 14

    position = sentence.find("warm");            //Line 15
    cout << "Line 16: " << position << endl;      //Line 16

    return 0;                                     //Line 17
}                                               //Line 18
```
```

# Sample Run:

```
Line 9: sentence = "Outside it is cloudy and warm."
Line 10: The position of "is" in sentence = 11
Line 11: The position of 's' in sentence = 3
Line 12: The position of "cloudy" in sentence = 14
Line 13: The position of "the" in sentence = 4294967295
Line 14: The first occurrence of 'i' in sentence
    after position 6 = 8
Line 16: Position = 25
```

The output of this program is self-explanatory. The details are left as an exercise for you. Notice that this program uses the static cast operator to output the value