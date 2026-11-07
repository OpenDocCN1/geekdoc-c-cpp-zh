```
```cpp
char setC[5] = {'A', 'E', 'I', 'O', 'U'};          //Line 9
ostream_iterator<char> screen(cout, " ");          //Line 10

cout << "Line 11: setA: ";                         //Line 11
copy(setA, setA + 5, screen);                       //Line 12
cout << endl;                                       //Line 13

cout << "Line 14: setB: ";                         //Line 14
copy(setB, setB + 10, screen);                      //Line 15
cout << endl;                                       //Line 16

cout << "Line 17: setC: ";                         //Line 17
copy(setC, setC + 5, screen);                       //Line 18
cout << endl;                                       //Line 19

if (includes(setB, setB + 10, setA, setA + 5))     //Line 20
    cout << "Line 21: setA is a subset of "        //Line 21
         << "setB." << endl;
else                                                //Line 22
    cout << "Line 23: setA is not a subset "       //Line 23
         << "of setB." << endl;

if (includes(setB, setB + 10, setC, setC + 5))     //Line 24
    cout << "Line 25: setC is a subset of "        //Line 25
         << "setB." << endl;
else                                                //Line 26
    cout << "Line 27: setC is not a subset "       //Line 27
         << "of setB." << endl;                    //Line 27

return 0;                                           //Line 28
}                                                   //Line 29
```
```

# **Sample Run:**

```
```text
Line 11: setA: A B C D E
Line 14: setB: A B C D E F I J K L
Line 17: setC: A E I O U
Line 21: setA is a subset of setB.
Line 27: setC is not a subset of setB.
```
```

The preceding output is self-explanatory. The details are left as an exercise for you.

The algorithm set_intersection is used to find the elements that are common to two ranges of elements. This algorithm has two forms, as given by the following prototypes:

```
```cpp
template <class inputItr1, class inputItr2,
          class outputItr>
outputItr set_intersection(inputItr1 first1, inputItr1 last1,
                          inputItr2 first2, inputItr2 last2,
                          outputItr destFirst);
```
```