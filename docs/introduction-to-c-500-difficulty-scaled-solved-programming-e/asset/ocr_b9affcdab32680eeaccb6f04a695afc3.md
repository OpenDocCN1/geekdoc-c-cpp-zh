# 22 • Exceptions 721
if(str[i] == '!' || str[i] == '$' || str[i] == '#')

```
if (dig < 3)
    throw 10;
    if (found == false)
        throw 20;
    return 0;
}
```

Let's see how the program works. Initially, the check_pswd() checks the length of the password. If it is less than six characters, the throw statement creates an exception and passes a literal string to the calling function, that is, main(). So, the type of exception is const char*. The throw statement terminates the check_pswd() and the program control is transferred to main(). In general, when an exception is thrown the implementation unwinds the stack frame to transfer control to the calling function that has the means to handle kind of exception. If the call to check_pswd() is made inside the try block, the program can catch the exception it creates. If the call was made outside the try block, the exceptions could not be caught.

The program now checks if there is a catch statement that matches the type. Then, the const char* catches the exception and executes the code. String "Error: Short length!" is passed to the msg parameter and it on the screen. With the continue statement the program continues with the next iteration of the loop and the break return to the program or some other approach, such as if the user enters an invalid password three times first. At each catch block, the program decides how to handle the exception. Note that if the const char block does not exist, the exception would have been caught by the catch(...) block and its code would be executed. If neither, the program would terminate.

If the password length is acceptable, check_pswd() checks if it contains less than three digits. If so, it creates an exception of int. Then, check_pswd() terminates and the int block in main() catches the exception. The code becomes 10 and the program displays the respective message. If the number of digits is valid, check_pswd() checks if the password contains any of !, $, or # characters. If not, it creates an exception of int, in the catch block the code becomes 20 and the program displays the message. As before, the continue statement causes the next loop iteration. Note that, in contrast to return which can only return one data type, throw can return different types of data.

If the password is accepted, check_pswd() does not create an exception and returns the value 0. The reason I chose to return a value is to show you which may also indicate if it was executed successfully or. Then the program skips the catch blocks and displays the password. The program runs until the user enters the end. Then, the break statement terminates the loop. Yes, I could write a simpler example, I wanted to show you that the break and continue statements inside a try-catch block work in the usual way.

Here is a simpler example. What does the following program display? Don't rush to give the answer, read the comment because I want the result.

```
#include <iostream> // Example 22.2

void f(int *p);

int main() {
    try {
        int i = 20;
        f(&i);
    }
```