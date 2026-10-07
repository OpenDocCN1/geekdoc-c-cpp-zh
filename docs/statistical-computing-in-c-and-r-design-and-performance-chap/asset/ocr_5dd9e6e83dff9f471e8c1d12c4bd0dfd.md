# MISCELLANEOUS TOPICS

Enter a new integer < 5 (q to quit)
Your integer is 2
Enter a new integer < 5 (q to quit)
All done

The try/catch mechanism as seen in the previous example certainly takes error handling to a higher level. But, from a practical perspective there is little that distinguishes your tryCatchExl program from what was accomplished previously with exit or assert. This is mostly due to the simplicity of the example and, frankly, makes the point that when some errors are encountered a simple error handling method will suffice. In more complicated situations, the try/catch approach has many features that may make it worth considering. For example, a function can throw objects as exception. This provides a convenient way to package diagnostic information that can be processed in the catch block. In the latter respect, there are also built-in classes that are used by C++ functions and can also be adapted to deal with some of the standard errors that are produced by user-defined functions. In general, an exception class can be expected to have a member function what reports the form of the error. When creating new objects from one of these classes, the argument supplied to the class constructor will determine the output from what.

As a case in point, consider the out_of_range exception class that is made available including the stdexcept header file used by some functions of the string class and the vector and deque container classes of Chapter 10 when an attempt is to access elements whose indices are not valid. The program below illustrates this with the string class insert method while providing another spin on using our catch function.

```
//tryCatchEx.cpp
#include <iostream>
#include <string>
#include <stdexcept>

using std::cout; using std::endl; using std::string;

void intCheck(const int i) throw(out_of_range){
    if(i > 5)
        throw std::out_of_range("intCheck");
    cout << "Your integer is " << i << endl;
}

int main(){
    string s;
    s = "Hi ya ll!";
    int n;
    std::cin >> n;
    try{
        cout << s.insert(n, "there " << endl;
        intCheck(n);
    }
    catch(std::out_of_range& e){
        cout << "Out of range " << e.what() << endl;
    }
    cout << "All done" << endl;

```