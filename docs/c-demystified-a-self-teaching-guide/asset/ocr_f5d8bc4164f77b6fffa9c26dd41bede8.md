Therefore, viewing the main function can provide an excellent overview of the order of events. Burying the main function beneath numerous other functions requires someone reviewing your code to hunt for main to obtain that overview. Additionally, in complex programs in which one function calls another function calls still another, the order in which to define these functions to avoid a compiler error can be confusing.

The solution of preference is to prototype every function, except main, which does not have to be prototyped since it is required by every program. The following program shows how to prototype the printMessage function in the Hello World program:

```
#include <iostream>
using namespace std;
void printMessage(void); // this is the prototype!

int main() {
    printMessage();
    return 0;
}
void printMessage(void) {
    cout << "Hello world!";
}
```

The prototype is above all function definitions. This ensures that the compiler, compiling the code from top to bottom, will encounter the prototype before any function.

The prototype is similar to a function header. The primary difference is that it has a semicolon at the end because it is a statement. By contrast, a function header must not be followed by a semicolon.

+   Note There are other differences between the prototype and the function header when, unlike, the parentheses following the function name includes one or more arguments. These differences will be discussed in the section "Sending Information to a Function" later in this chapter.