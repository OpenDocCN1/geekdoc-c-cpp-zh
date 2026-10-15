```
15  // use cin to input characters into buffer1
16  cout << "Enter a sentence:" << endl;
17  cin >> buffer1;
18
19  // display buffer1 contents
20  cout << "\nThe string read with cin was:" << endl
21      << buffer1 << endl << endl;
22
23  // use cin.get to input characters into buffer2
24  cin.get( buffer2, SIZE );
25
26  // display buffer2 contents
27  cout << "The string read with cin.get was:" << endl
28      << buffer2 << endl;
29      return 0;
30  } // end main
```

Enter a sentence:
**Contrasting string input with cin and cin.get**

The string read with cin was:
Contrasting

The string read with cin.get was:
string input with cin and cin.get

Fig. 15.5 | Input of a string using cin with stream extraction contrasted with input using cin.get. (Part 2 of 2.)

# Using Member Function getline

Member function getline operates similarly to the third version of the get member function and inserts a null character after the line in the character array. The getline function removes the delimiter from the stream (i.e., reads the character and discards it), but does not store it in the character array. The program of Fig. 15.6 demonstrates the use of the getline member function to input a line of text (line 15).

```
1  // Fig. 15.6: Fig15_06.cpp
2  // Inputting characters using cin member function getline.
3  #include <iostream>
4  using std::cin;
5  using std::cout;
6  using std::endl;
7
8  int main()
9  {
10     const int SIZE = 80;
11     char buffer[ SIZE ]; // create array of 80 characters
12
```

Fig. 15.6 | Inputting character data with cin member function getline. (Part 1 of 2.)