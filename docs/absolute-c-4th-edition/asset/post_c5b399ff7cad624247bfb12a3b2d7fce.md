
# SYNTAX

```
try
{
    Some_Statements
    <Either some code with a throw statement or
    a function invocation that might throw an exception>
    Some_More_Statements
}
catch(Type e)
{
    < Code to be performed if a value of the
    catch-block parameter type is thrown in the try block>
}
```

# EXAMPLE

See Display 18.2 for an example.

# Self-Test Exercises

+   1. What output is produced by the following code?

```
int waitTime = 46;

try
{
    cout << "Try block entered.\n";
    if (waitTime > 30)
        throw waitTime;
    cout << "Leaving try block.\n";
}

catch(int thrownValue)
{
    cout << "Exception thrown with\n"
         << "waitTime equal to " << thrownValue << endl;
}
cout << "After catch block" << endl;
```

+   2. What would be the output produced by the code in Self-Test Exercise 1 if we made the following change? Change the line
+   int waitTime = 46;
+   to
+   int waitTime = 12;

+   3. In the code given in Self-Test Exercise 1, what is the throw statement?
+   4. What happens when a throw statement is executed? (Tell what happens in general, not simply what happens in the code in Self-Test Exercise 1 or some other sample code.)
+   5. In the code given in Self-Test Exercise 1, what is the try block?
+   6. In the code given in Self-Test Exercise 1, what is the catch block?
+   7. In the code given in Self-Test Exercise 1, what is the catch-block parameter?

# DEFINING YOUR OWN EXCEPTION CLASSES

A throw statement can throw a value of any type. A common thing to do is to define a class whose objects can carry the precise kinds of information you want thrown to the catch block. An even more important reason for defining a specialized exception class is so that you can have a different type to identify each possible kind of exceptional situation.

An exception class is just a class. What makes it an exception class is how it is used. Still, it pays to take some care in choosing an exception class’s name and other details.

Display 18.3 contains an example of a program with a programmer-defined exception class. This is just a toy program to illustrate some C++ details about exception handling. It uses much too much machinery for such a simple task, but it is an otherwise uncluttered example of some C++ details.

Notice the throw statement, reproduced in what follows:

```
throw NoMilk(donuts);
```

The part NoMilk(donuts) is an invocation of a constructor for the class NoMilk. The constructor takes one int argument (in this case, donuts) and creates an object of the class NoMilk. That object is then thrown.

# MULTIPLE THROWS AND CATCHES

A try block can potentially throw any number of exception values, which can be of differing types. In any one execution of the try block, at most one exception will be thrown (since a throw statement ends the execution of the try block), but different types of exception values can be thrown on different occasions when the try block is executed. Each catch block can only catch values of one type, but you can catch exception values of differing types by placing more than one catch block after a try block. For example, the program in Display 18.4 has two catch blocks after its try block.

Note that there is no parameter in the catch block for DivideByZero. If you do not need a parameter, you can simply list the type with no parameter. This is discussed a bit more in the programming tip section entitled "Exception Classes Can Be Trivial."

# Display 18.3 Defining Your Own Exception Class

```
#include <iostream>
using std::cin;
using std::cout;

class NoMilk
{
public:
    NoMilk() {}
    NoMilk(int howMany) : count(howMany) {}
    int getCount() const { return count; }
private:
    int count;
};

int main()
{
    int donuts, milk;
    double dpg;
    try
    {
        cout << "Enter number of donuts:\n";
        cin >> donuts;
        cout << "Enter number of glasses of milk:\n";
        cin >> milk;

        if (milk <= 0)
            throw NoMilk(donuts);

        dpg = donuts/static_cast<double>(milk);
        cout << donuts << " donuts\n"
             << milk << " glasses of milk.\n"
             << "You have " << dpg
             << " donuts for each glass of milk.\n";
    }
    catch(NoMilk e)
    {
        cout << e.getCount() << " donuts, and No Milk!\n"
             << "Go buy some milk.\n";
    }
    cout << "End of program.\n";
    return 0;
}
```

This is just a toy example to learn C++ syntax. Do not take it as an example of good typical use of exception handling.

The sample dialogues are the same as in Display 18.2.

# Display 18.4. Catching Multiple Exceptions (part 1 of 2)

```
```cpp
#include <iostream>
#include <string>
using std::cin;
using std::cout;
using std::endl;
using std::string;

class NegativeNumber
{
public:
    NegativeNumber() {}
    NegativeNumber(string theMessage): message(theMessage) {}
    string getMessage() const { return message; }
private:
    string message;
};

class DivideByZero
{};

int main()
{
    int pencils, erasers;
    double ppe; //pencils per eraser

    try
    {
        cout << "How many pencils do you have?\n";
        cin >> pencils;
        if (pencils < 0)
            throw NegativeNumber("pencils");

        cout << "How many erasers do you have?\n";
        cin >> erasers;
        if (erasers < 0)
            throw NegativeNumber("erasers");

        if (erasers != 0)
            ppe = pencils/static_cast<double>(erasers);
        else
            throw DivideByZero();

        cout << "Each eraser must last through "
             << ppe << " pencils.\n";
    }
```
```

> *Exception classes can have their own interface and implementation files and can be put in a namespace. This is another example.*

## 1. 引言

在当今快速发展的技术时代，人工智能（AI）已经成为推动社会进步的重要力量。从智能助手到自动驾驶，AI 技术正在深刻改变我们的生活方式和工作模式。本文旨在探讨 AI 技术的最新进展及其在各领域的应用前景。

## 2. AI 技术的主要领域

- 机器学习：通过数据训练模型，使系统能够自动学习和改进。
- 深度学习：基于神经网络的多层结构，处理复杂模式识别任务。
- 自然语言处理：使计算机能够理解、解释和生成人类语言。
- 计算机视觉：让机器能够“看懂”图像和视频内容。

## 3. 应用场景

| 领域 | 应用示例 | 影响程度 |
|------|----------|----------|
| 医疗 | 疾病诊断、药物研发 | 高 |
| 交通 | 自动驾驶、智能调度 | 高 |
| 教育 | 个性化学习、智能辅导 | 中 |
| 金融 | 风险评估、欺诈检测 | 高 |

> > “AI 不是要取代人类，而是要增强人类的能力。” —— 某知名 AI 研究者

综上所述，AI 技术正在多个领域展现出巨大的潜力。未来，随着算法的不断优化和计算能力的提升，AI 将在更多场景中发挥关键作用，为人类社会带来更多福祉。

# Pitfall
CATCH THE MORE SPECIFIC EXCEPTION FIRST

When catching multiple exceptions, the order of the catch blocks can be important. When an exception value is thrown in a try block, the catch blocks that follow it are tried in order, and the first one that matches the type of the exception thrown is the one that is executed.

For example, the following is a special kind of catch block that will catch a thrown value of any type:

```
catch (...)
{
    <Place whatever you want in here.>
}
```

The three dots do not stand for something omitted. You actually type in those three dots in your program. This makes a good default catch block to place after all other catch blocks. For example, we could add it to the catch blocks in Display 18.4 as follows:

```
catch(NegativeNumber e)
{
    cout << "Cannot have a negative number of "
         << e.getMessage() << endl;
}
catch(DivideByZero)
{
    cout << "Do not make any mistakes.\n";
}
catch (...)
{
    cout << "Unexplained exception.\n";
}
```

However, it only makes sense to place this default catch block at the end of a list of catch blocks. For example, suppose we instead used:

```
catch(NegativeNumber e)
{
    cout << "Cannot have a negative number of "
         << e.getMessage() << endl;
}
catch (...)
{
    cout << "Unexplained exception.\n";
}
catch(DivideByZero)
{
    cout << "Do not make any mistakes.\n";
}
```

With this second ordering, an exception (a thrown value) of type `NegativeNumber` will be caught by the `NegativeNumber` catch block as it should be. However, if a value of type `DivideByZero` were thrown, it would be caught by the block that starts `catch(...)`. So, the `DivideByZero` catch block could never be reached. Fortunately, most compilers will tell you if you make this sort of mistake.

# Tip — EXCEPTION CLASSES CAN BE TRIVIAL

Below we have reproduced the definition of the exception class `DivideByZero` from Display 18.4:

```
class DivideByZero
{};
```

This exception class has no member variables and no member functions (other than the default constructor). It has nothing but its name, but that is useful enough. Throwing an object of the class `DivideByZero` can activate the appropriate catch block, as it does in Display 18.4.

When using a trivial exception class, you normally do not have anything you can do with the exception (the thrown value) once control gets to the catch block. The exception is just being used to get you to the catch block. Thus, you can omit the catch-block parameter. In fact, you can omit the catch-block parameter any time you do not need it, whether the exception type is trivial or not.

# THROWING AN EXCEPTION IN A FUNCTION

Sometimes it makes sense to delay handling an exception. For example, you might have a function `f` that codes that throws an exception if there is an attempt to divide by zero, but you may not want to catch the exception in that function. Perhaps some programs that use that function should simply end if the exception is thrown, and other programs that use the function should do something else. Thus, you would not know what to do with the exception if you caught it inside the function. In these cases, it makes sense to not catch the exception in the function definition, but instead to have any program (or other code) that uses the function place the function invocation in a try block and catch the exception in a catch block that follows that try block.

Look at the program in Display 18.5. It has a try block, but there is no throw statement visible in the try block. The statement that does the throwing in that program is

```
if (bottom == 0)
    throw DivideByZero();
```

This statement is not visible in the try block. However, it is in the try block in terms of program execution, because it is in the definition of the function `safeDivide` and there is an invocation of `safeDivide` in the try block.
