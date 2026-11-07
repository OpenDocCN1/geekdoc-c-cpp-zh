```
cout << "Line 13: After insert; firstString = "
     << firstString << endl;                  //Line 13

cout << "Line 14: secondString = " << secondString
     << endl;                                 //Line 14
secondString.insert(11, 5, '!');              //Line 15
cout << "Line 16: After insert; secondString = "
     << secondString << endl;                 //Line 16

cout << "Line 17: thirdString = " << thirdString
     << endl;                                 //Line 17
thirdString.replace(0, 5, str2);              //Line 18
cout << "Line 19: After replace, thirdString = "
     << thirdString << endl;                  //Line 19

return 0;                                     //Line 20
}                                             //Line 21
```

# Sample Run:

```
Line 11: firstString = Cloudy and warm.
Line 13: After insert; firstString = Cloudy and very warm.
Line 14: secondString = Hello there
Line 16: After insert; secondString = Hello there!!!!!
Line 17: thirdString = Henry is in programming I.
Line 19: After replace, thirdString = Lisa is in programming I.
```

The output of this program is self-explanatory. The details are left as an exercise for you.

# EXAMPLE 7-17 (substr FUNCTION)

Consider the following statements:

```
string sentence;

string str;

sentence = "It is cloudy and warm.";
```

Next, we show the effect of the substr function.

| Statement | Effect |
|---|---|
| cout << sentence.substr(0, 5) << endl; | Outputs: It is |
| cout << sentence.substr(6, 6) << endl; | Outputs: cloudy |
| cout << sentence.substr(6, 16) << endl; | Outputs: cloudy and warm. |
| cout << sentence.substr(17, 10) << endl; | Outputs: warm. |
| cout << sentence.substr(3, 6) << endl; | Outputs: is clo |
| str = sentence.substr(0, 8); | str = "It is cl" |
| str = sentence.substr(2, 10); | str = " is cloudy" |