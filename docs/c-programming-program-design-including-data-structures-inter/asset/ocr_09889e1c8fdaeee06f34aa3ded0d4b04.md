```
int main()
{
    string sentence = "Outside it is cloudy and warm.";        //Line 1
    string str = "cloudy";                                  //Line 2

    string::size_type position;                              //Line 3

    cout << "Line 4: sentence = \"" << sentence
         << "\n" << endl;                                   //Line 4

    cout << "Line 5: The position of \"is\" in sentence = "
         << static_cast<unsigned int> (sentence.find("is"))
         << endl;                                             //Line 5

    cout << "Line 6: The position of 's' in sentence = "
         << static_cast<unsigned int> (sentence.find('s'))
         << endl;                                             //Line 6

    cout << "Line 7: The position of \"" << str
         << "\" in sentence = "
         << static_cast<unsigned int> (sentence.find(str))
         << endl;                                             //Line 7

    cout << "Line 8: The position of \"the\" in sentence = "
         << static_cast<unsigned int> (sentence.find("the"))
         << endl;                                             //Line 8

    cout << "Line 9: The first occurrence of \'i\' in "
         << "sentence \n        after position 6 = "
         << static_cast<unsigned int> (sentence.find('i', 6))
         << endl;                                             //Line 9

    position = sentence.find("warm");                         //Line 10
    cout << "Line 11: Position = "
         << position << endl;                                 //Line 11

    return 0;                                                 //Line 12
}
```

# Sample Run:

```
Line 4: sentence = "Outside it is cloudy and warm."
Line 5: The position of "is" in sentence = 11
Line 6: The position of 's' in sentence = 3
Line 7: The position of "cloudy" in sentence = 14
Line 8: The position of "the" in sentence = 4294967295
Line 9: The first occurrence of 'i' in sentence
         after position 6 = 8
Line 11: Position = 25
```