# Answers to Self-Review Exercises

+   2.1  a) main. b) left brace ({), right brace (}). c) semicolon. d) newline. e) if.

+   2.2  a) False. Comments do not cause any action to be performed when the program is executed. They're used to document programs and improve their readability.
+       b) True.
+       c) True.
+       d) True.
+       e) False. C++ is case sensitive, so these variables are unique.
+       f) True.
+       g) True.
+       h) False. The operators *, / and % have the same precedence, and the operators + and - have a lower precedence.
+       i) False. One statement with cout and multiple \n escape sequences can print several lines.

+   2.3  a) int c, thisIsAVariable, q76354, number;
+       b) std::cout << "Enter an integer: ";
+       c) std::cin >> age;
+       d) if ( number != 7 )
+              std::cout << "The variable number is not equal to 7\n";
+       e) std::cout << "This is a C++ program\n";
+       f) std::cout << "This is a C++\nprogram\n";
+       g) std::cout << "This\nis\na\nC++\nprogram\n";
+       h) std::cout << "This\tis\ta\tC++\tprogram\n";

+   2.4  a) // Calculate the product of three integers
+       b) int x;
+          int y;
+          int z;
+          int result;
+       c) cout << "Enter three integers: ";
+       d) cin >> x >> y >> z;
+       e) result = x * y * z;
+       f) cout << "The product is " << result << endl;
+       g) return 0;

2.5  (See program below.)

```
~~~cpp
1  // Calculate the product of three integers
2  #include <iostream> // allows program to perform input and output
3  using namespace std; // program uses names from the std namespace
4
5  // function main begins program execution
6  int main()
7  {
8     int x; // first integer to multiply
9     int y; // second integer to multiply
10    int z; // third integer to multiply
11    int result; // the product of the three integers
12
13    cout << "Enter three integers: "; // prompt user for data
14    cin >> x >> y >> z; // read three integers from user
15    result = x * y * z; // multiply the three integers; store result
16    cout << "The product is " << result << endl; // print result; end line
17 } // end function main
~~~
```