# PROGRAM 13.2 get() and put() functions

```
```cpp
//GetPut.cpp
#include <iostream>
#include <string>
#include <fstream>
#include <iomanip>
using namespace std;

int main()
{
	char ch;
	ofstream EntryFile("FewLines.dat");
	while(true)
	{
		cin.get(ch);
		if(ch == '$') break;
		EntryFile << ch;
	}
	EntryFile.close();
	ifstream DisplayFile("FewLines.dat");
	while(!DisplayFile.eof())
	{
		// Do not skip white space
		DisplayFile.unsetf(ios::skipws);
		DisplayFile >> ch;
		cout << ch;
	}
	DisplayFile.close();
	return 0;
}
```
```

Input

The battle
between One and Another
is
between light and darkness
between truthfulness and falsehood
between duty and ego
$

Output

The battle
between One and Another
is
between light and darkness
between truthfulness and falsehood
between duty and ego



The program begins with opening a file in the write mode, so that a few lines can be written into it.

ofstream EntryFile("FewLines.dat");

The put() function is called to write characters into this file. One can read a character, stop if $ is encountered or continue otherwise, and write that character in the EntryFile using three statements as follows. Look at how << is used to enter data in a file.