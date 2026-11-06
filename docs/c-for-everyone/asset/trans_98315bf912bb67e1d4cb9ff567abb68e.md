
对于隐式参数上的成员函数，你不需要指定参数，只需写出成员函数名：

```
set_answer(num_str);
```

编译器将此调用解释为

```
implicit parameter.set_answer(num_str);
```

![](img/5e58fb4c840712efd6ed6fa82bb97f57_476_0.png)

## 自测

- 6. 假设 q 是 Question 类的对象，cq 是 ChoiceQuestion 类的对象。以下哪些调用是合法的？
  - a. `q.set_answer(response)`
  - b. `cq.set_answer(response)`
  - c. `q.add_option(option, true)`
  - d. `cq.add_option(option, true)`

- 7. 定义一个 Manager 类，它继承自 Employee 类，并添加一个数据成员 bonus 用于存储工资奖金。省略构造函数声明。

- 8. 假设 Employee 类定义如下：

  ```
  class Employee
  {
  public:
      Employee();
      void set_name(string new_name);
      void set_base_salary(double new_salary);
      string get_name();
      double get_salary() const;
  private:
      string name;
      double base_salary;
  };
  ```

  自测第 7 题中的 Manager 类拥有哪些数据成员？

- 9. 定义一个 Manager 类，它继承自 Employee 类并覆盖 `get_salary` 函数。

- 10. 自测第 9 题中的 Manager 类继承了哪些成员函数？

## 实践练习

现在你可以尝试本章末尾的练习：P10.2、P10.6。

## 私有继承

### 常见错误 10.1

![](img/5e58fb4c840712efd6ed6fa82bb97f57_476_1.png)

一个常见错误是忘记关键字 `public`，它必须跟在派生类名称后的冒号之后。

```
class ChoiceQuestion : Question // Error
{
    ...
};
```

类定义可以编译通过。ChoiceQuestion 仍然继承自 Question，但它是 *私有* 继承。也就是说，只有 ChoiceQuestion 的成员函数才能调用 Question 的成员函数。当其他函数在 ChoiceQuestion 对象上调用 Question 成员函数时，编译器会将其标记为错误：

```
int main()
{
```

其他汽车在驾驶和加油方面。它们只是有更好的燃油效率。一个带有数据成员的简单 Car 类

```
double miles_per_gallon;
```

就完全足够了。
然而，如果你编写一个展示如何修理不同类型车辆的程序，那么单独一个 HybridCar 类就有意义了。在修理方面，混合动力汽车的行为与其他汽车不同。

### 专题 10.1：调用基类构造函数

![](img/5e58fb4c840712efd6ed6fa82bb97f57_478_0.png)

除非另有指定，基类数据成员将使用默认构造函数进行初始化。

考虑构造派生类对象的过程。派生类构造函数只能初始化派生类的数据成员。但基类数据成员也需要被初始化。除非你另有指定，否则基类数据成员会使用基类的默认构造函数进行初始化。

为了指定另一个构造函数，你需要使用初始化列表，如专题 9.1 所述。在初始化列表中指定基类的名称和构造参数。例如，假设 Question 基类有一个用于设置问题文本的构造函数。下面是一个派生类构造函数如何调用该基类构造函数：

```
ChoiceQuestion::ChoiceQuestion(string question_text)
    : Question(question_text)
{
}
```

派生类构造函数在执行 { } 内的代码之前调用基类构造函数。

在我们的示例程序中，我们使用了基类的默认构造函数。然而，如果基类没有默认构造函数，你必须使用初始化列表语法。

派生类的构造函数可以向基类构造函数提供参数。

### 语法 10.2：带基类初始化器的构造函数

```
// The base-class constructor is called first.
ChoiceQuestion::ChoiceQuestion(string question_text)
    : Question(question_text)
{
    // This block can contain additional statements.
}
// If you omit the base-class constructor call, the default constructor is invoked.
```

## 10.3 覆盖成员函数

派生类继承基类的成员函数。如果你对所继承成员函数的行为不满意，可以通过在派生类中指定新的实现来**覆盖**它。

> 派生类可以从基类继承函数，也可以通过提供另一实现来覆盖它。

考虑 `ChoiceQuestion` 类的 display 函数。它需要覆盖基类的 display 函数以显示答案选项。具体来说，派生类函数需要

- **显示问题文本。**
- **显示答案选项。**

第二部分很容易，因为答案选项是派生类的一个数据成员。

```
void ChoiceQuestion::display() const
{
    // Display the question text

    // Display the answer choices
    for (int i = 0; i < choices.size(); i++)
    {
        cout << i + 1 << ": " << choices[i] << endl;
    }
}
```

但是如何获取问题文本呢？你不能直接访问基类的 text 成员，因为它是私有的。

相反，你可以调用基类的 display 函数。

```
void ChoiceQuestion::display() const
{
    // Display the question text
    display();  // Invokes implicit parameter.display()
    // Display the answer choices
    ...
}
```

然而，这并不完全可行。由于 `ChoiceQuestion::display` 的隐式参数类型是 `ChoiceQuestion`，并且在 `ChoiceQuestion` 类中有一个名为 `display` 的函数，该函数将被调用——但这正是你当前正在编写的函数！该函数会一遍又一遍地调用自身。

要显示问题文本，你必须更明确地指定要调用哪个名为 `display` 的函数。你需要的是 `Question::display`：

```
void ChoiceQuestion::display() const
{
    // Display the question text
    Question::display();  // OK
    // Display the answer choices
    ...
}
```

当你覆盖一个函数时，通常希望扩展基类版本的功能。因此，你通常需要在扩展之前调用基类版本。要调用它，你需要使用 `BaseClass::function` 表示法。但是，你没有义务调用基类函数。有时，派生类会覆盖基类函数并指定完全不同的功能。

> 使用 `BaseClass::function` 表示法来显式调用基类函数。

下面是一个完整程序，它显示一个普通的 Question 对象和一个 ChoiceQuestion 对象。（你已经见过的 Question 类定义放在 `question.h` 中，实现在 `question.cpp` 中。）这个示例展示了如何利用继承从基类形成更专门的类。

ch10/quiz2/test.cpp

```cpp
#include <iostream>
#include <sstream>
#include <vector>
#include "question.h"

class ChoiceQuestion : public Question
{
public:
   /**
      Constructs a choice question with no choices.
   */
   ChoiceQuestion();

   /**
      Adds an answer choice to this question.
      @param choice the choice to add
      @param correct true if this is the correct choice, false otherwise
   */
   void add_choice(string choice, bool correct);

   void display() const;
private:
   vector<string> choices;
};

ChoiceQuestion::ChoiceQuestion()
{
}

void ChoiceQuestion::add_choice(string choice, bool correct)
{
   choices.push_back(choice);
   if (correct)
   {
      // Convert choices.size() to string
      ostringstream stream;
      stream << choices.size();
      string num_str = stream.str();
      set_answer(num_str);
   }
}

void ChoiceQuestion::display() const
{
   // Display the question text
   Question::display();
   // Display the answer choices
   for (int i = 0; i < choices.size(); i++)
   {
      cout << i + 1 << ": " << choices[i] << endl;
   }
}

int main()
{
   string response;
   cout << boolalpha;
}
```
