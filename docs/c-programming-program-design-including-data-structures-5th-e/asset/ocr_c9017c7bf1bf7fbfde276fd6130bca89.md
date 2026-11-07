9. Consider the following C++ code:

```
```cpp
string str1;
string str2;
char ch;

cin >> str1;
str2 = str1;
cin >> ch;
str2[0] = ch;
cout << str1 << " " << str2 << endl;
```
```

Answer the following questions.

+   a. What is the output if the input is `Hello J`?
+   
+   b. What is the output if the input is `Bingo R`?
+   
+   c. What is the output if the input is `Sunny B`?

10. Suppose that you have the following statements:

```
```cpp
string str1, str2;

cin >> str1 >> str2;

if (str1 == str2)
    cout << str1 + '!' << endl;
else if (str1 > str2)
    cout << str1 + " > " + str2 << endl;
else
    cout << str1 + " < " + str2 << endl;
```
```

Answer the following questions.

+   a. What is the output if the input is `diamond diamond`?
+   
+   b. What is the output if the input is `diamond gold`?
+   
+   c. What is the output if the input is `silver gold`?

11. What is the output of the following program?

```
```cpp
#include <iostream>
#include <string>

using namespace std;

int main()
{
    string str1 = "Amusement Park";
    string str2 = "Going to";
    string str3 = "the";
    string str;

    cout << str2 + ' ' + str3 + ' ' + str1 << endl;
    cout << str1.length() << endl;
    cout << str1.find('P') << endl;
    cout << str1.substr(1, 5) << endl;
```
```