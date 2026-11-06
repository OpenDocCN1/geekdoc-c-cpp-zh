
computer to deduce it for you. (This example uses the same `DemangleIt()` function described in the “Understanding the Role of auto” section of Chapter 1 of this minibook.)

### LISTING 2-1: Deciding Between a Deduced or Specific Return Type

```cpp
#include <iostream>
#include <typeinfo>
#include <memory>
#include <cxxabi.h>

using namespace std;

string DemangleIt(const char* Mangled) {
    int Status;
    unique_ptr<char[], void(*)(void*)> Result(
        abi::__cxa_demangle(Mangled, 0, 0, &Status), free);
    return Result.get() ? string(Result.get()) : "Error";
}

void ShowType(function<float(double)> lambda) {
    cout << "Input has a value of: " << lambda(2.6) << endl;
    cout << "Input has type of: " <<
        DemangleIt(typeid(lambda(2.6)).name()) << endl;
}

void ShowChar(function<char(int)> lambda){
    cout << "Input has a value of: " << lambda(7) << endl;
}

int main() {
    ShowType([](int x) -> int {return int(x * x);});
    ShowType([](double x) -> int {return int(x * x);});
    ShowType([](double x) -> double {return x * x;});
    ShowType([](double x) {return float(x * x);});
    ShowType([](double x) {return x > 2 ? true : false;});
    ShowType([](int x) -> char {return char(x * 10);});
    ShowChar([](int x) -> char {return char(x * 10);});
    return 0;
}
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_422_0.png)

The input argument for the functions in this example is `function<>`. When using `function<>`, you specify a return type, even if the return type is `void`, and any input types, or empty parentheses, `()`, when the function doesn’t need one. Part of the problem with both `ShowType()` and `ShowChar()` is that the `function<>` declaration doesn’t allow use of `auto`, so you get whatever type you define, as you see later in the example.

The `ShowType()` and `ShowChar()` functions both show the value of `lambda()` when you provide a specific input value to the lambda expression. The `ShowType()` function also outputs the type of the value output by the function, and you’ll see the importance of this output in a moment.

The lambda functions are of the two const types described in the “Defining the parts of a lambda expression” section, earlier in this chapter. Some specify a return type; others don’t. Note that the first two lambda expressions both provide an int output, but one takes an int as input and the other takes a double. Playing with input and output types like this can help you understand the effects of decisions that you make when using lambda expressions. Note that the last three lambda expressions don’t actually return a numeric type. The first of these returns a bool and the last two return char.

![](img/128ab511de4e7360e167e3b15cdd5dd0_422_1.png)

You probably think that one or more of these lambda expressions will fail, especially given the input values used in `ShowType()` and `ShowChar()`. However, they all do work, as shown in the somewhat surprising output here:

```
Input has a value of: 4
Input has type of: float
Input has a value of: 6
Input has type of: float
Input has a value of: 6.76
Input has type of: float
Input has a value of: 6.76
Input has type of: float
Input has a value of: 1
Input has type of: float
Input has a value of: 20
Input has type of: float
Input has a value of: F
```

The compiler seems adept at making the lambda expressions work even when they really shouldn’t. For example, the first lambda expression accepts an int as input and produces an int as output, so the input is truncated, which results in an output of 4. The second lambda expression truncates the output as an int, so now you see 6 from what should be the same calculation, which should actually produce a value of 6.76, as shown in the next two outputs. The bool output is a value of 1 and the char output is a value of 20, neither of which reflects their true types. However, the really odd thing is that the type of all these outputs is float (the default as explained in the next section); it doesn't matter what the lambda expression actually provided as output. The point is that you need to exercise care in the construction of both the lambda expression and the function that receives it to obtain the desired result.

## Using the auto keyword with lambda expressions

The auto keyword can save you a great deal of pain when working with lambda expressions, plus it can help you avoid some common problems with getting the result you want. The UseAuto example, shown in Listing 2-2, is a reworking of the example in Listing 2-1, shown earlier. However, even though the example works in a similar manner, the output is different because of the use of auto.

### LISTING 2-2: Performing Tasks Using auto

```cpp
#include <iostream>
#include <typeinfo>
#include <memory>
#include <cxxabi.h>

using namespace std;

string DemangleIt(const char* Mangled) {
    int Status;
    unique_ptr<char[], void(*)(void*)> Result(
        abi::__cxa_demangle(Mangled, 0, 0, &Status), free);
    return Result.get() ? string(Result.get()) : "Error";
}

void ShowData(auto lambda) {
    cout << "Input has a value of: " << lambda(3.6) << endl;
    cout << "Input has type of: " <<
        DemangleIt(typeid(lambda(3.6)).name()) << endl;
}

int main() {
    ShowData([](int x) -> int {return int(x * x);});
    ShowData([](double x) -> int {return int(x * x);});
    ShowData([](double x) -> double {return x * x;});
    ShowData([](double x) {return float(x * x);});
    ShowData([](double x) {return x > 2 ? true : false;});
    ShowData([](double x) -> char {return char(x * 10);});

    return 0;
}
```

When you run this example, you see that the auto keyword enables you to obtain results specific to the input. Here is what you see in this case (which you can compare to the output in the previous section):

```
Input has a value of: 9
Input has type of: int
Input has a value of: 12
Input has type of: int
Input has a value of: 12.96
Input has type of: double
Input has a value of: 12.96
Input has type of: float
Input has a value of: 1
Input has type of: bool
Input has a value of: $
Input has type of: char
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_424_0.png)

By giving up control over the form of the input to ShowData(), you also preserve the types of the various inputs. Each of the outputs is now of the correct type, and the char output (last) actually appears as a character rather than a number. However, there isn’t a best solution — only the solution that works to meet your specific requirements. You therefore need to keep the function<> method described in the previous section in mind.

Lest you think that someone could pass anything to ShowData(), you can try, but you won’t be successful. If you were to pass something like ShowData(14), the compiler would output an error message of 'lambda' cannot be used as a function. Even though you’re using auto, the auto is still expecting a function as input.

## Using lambda expressions as macros

You can assign a lambda expression to a variable and then use the variable as a kind of macro. This technique can make it a lot easier to perform some repetitive tasks that seem to appear everywhere, but take little code. The CreateMacro example, shown in Listing 2–3, demonstrates this approach.

### LISTING 2-3: Creating a Macro

```cpp
#include <iostream>

using namespace std;

int main(){
    auto f = [](auto Input) { cout << Input << endl;};

    f("Hello");
    f(221);
    f(true);
    f(99 / 3);
    f(char(65));
    f(int(15/4));
    return 0;
}
```

The code in this example creates a simple lambda expression that outputs the input expression, whatever it might be, to the screen. To make the macro work, you use auto in two contexts, both as the type of the variable holding the macro and as the input. Here’s the output you see:

```
Hello
221
1
33
A
3
```

## Developing with Lambda Expressions

The previous sections of the chapter give you an idea of how lambda expressions work. In the following sections of the chapter, you see how to implement certain lambda expression techniques in a more advanced manner that you might use within application code.
