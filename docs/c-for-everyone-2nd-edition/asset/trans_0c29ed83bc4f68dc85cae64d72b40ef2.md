

## ch10/quiz2/test.cpp

```cpp
#include <iostream>
#include <sstream>
#include <vector>
#include "question.h"

class ChoiceQuestion : public Question
{
public:
   /*
     Constructs a choice question with no choices.
   */
   ChoiceQuestion();

   /*
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

- 13. 再次查看 `add_choice` 函数的实现，它调用了基类的 `set_answer` 函数。为什么不需要调用 `Question::set_answer`？
- 14. 在自测 9 的 Manager 类中，重写 `get_name` 函数，使管理者的名字前带有一个 `*`（例如 *Lin, Sally*）。
- 15. 在自测 9 的 Manager 类中，重写 `get_salary` 函数，使其返回工资与奖金之和。

**实践练习**  现在你可以尝试本章末尾的这些练习：R10.12、P10.1。

![](img/23fb3582e93ebc95909e1de029c3d388_482_0.png)

## 忘记基类名

扩展基类函数功能时的一个常见错误是忘记基类名。例如，要计算经理的工资，先获取底层 `Employee` 对象的工资，再加上奖金：

```cpp
double Manager::get_salary() const
{
    double base_salary = get_salary();
        // Error—should be Employee::get_salary()
    return base_salary + bonus;
}
```

这里的 `get_salary()` 指的是应用于该成员函数隐式参数的 `get_salary` 函数。隐式参数的类型是 Manager，并且存在一个 `Manager::get_salary` 函数，因此会调用该函数。当然，这是对我们正在编写的函数的递归调用。相反，你必须指定想要调用哪个 `get_salary` 函数。在这种情况下，需要显式调用 `Employee::get_salary`。

每当从派生类函数中调用同名的基类函数时，务必给出函数的完整名称，包括基类名。

## 10.4 虚函数与多态

在前面的小节中，你看到了继承的一个重要用途：从基类形成更专门的类。在接下来的小节中，你将看到继承更强大的应用：处理类型和行为可在运行时变化的对象。这种行为的差异通过虚函数实现。当你在对象上调用虚函数时，C++ 运行时系统会根据对象所属的类来确定应调用哪个实际的成员函数。

在接下来的小节中，你将了解为什么需要使用指针来访问类可在运行时变化的那些对象，以及虚函数如何为给定对象选择适当的成员函数。

### 10.4.1 切片问题

在本节中，我们将讨论一个问题，当你处理属于类层次结构中不同类的对象集合时，这个问题经常出现。

如果你查看 quiz2/test.cpp 的 main 函数，你会发现有一些重复代码用于显示每个问题并检查回答。如果将所有问题收集到一个数组中，并且可以用循环将它们呈现给用户，那会更好：

```cpp
const int QUIZZES = 2;
Question quiz[QUIZZES];
quiz[0].set_text("Who was the inventor of C++?");
quiz[0].set_answer("Bjarne Stroustrup");
ChoiceQuestion cq;
cq.set_text("In which country was the inventor of C++ born?");
cq.add_choice("Australia", false);
...
quiz[1] = cq;

for (int i = 0; i < QUIZZES; i++)
{
    quiz[i].display();
    cout << "Your answer: ";
    getline(cin, response);
    cout << quiz[i].check_answer(response) << endl;
}
```

数组 quiz 保存 `Question` 类型的对象。编译器认识到 `ChoiceQuestion` 是 `Question` 的一种特殊情况。因此，它允许从选择题到问题的赋值：

```cpp
quiz[1] = cq;
```

然而，一个 `ChoiceQuestion` 对象有三个数据成员，而一个 `Question` 对象只有两个。没有空间存储派生类的数据。当你将派生类对象赋值给基类变量时，这些数据就会被 *切掉*（见图 5）。

如果运行生成的程序，选项不会被显示：

```
Who was the inventor of C++?
Your answer: Bjarne Stroustrup
true
In which country was the inventor of C++ born?
Your answer:
```

对于需要操作继承层次结构中混合类的对象的代码来说，这个问题非常典型。派生类对象通常比基类对象大，而不同派生类的对象具有不同的大小。对象数组无法处理这种大小变化。

将派生类对象转换为基类时，派生类数据会被切掉。

![](img/23fb3582e93ebc95909e1de029c3d388_483_0.png)

**图 5**  切掉派生类数据

### 10.4.3 虚函数

当你收集类层次结构中不同类的对象，然后调用成员函数时，你希望应用适当的成员函数。例如，当你对一个恰好指向 `ChoiceQuestion` 的 `Question*` 指针调用 display 成员函数时，你希望显示各个选项。

出于效率原因，这不是 C++ 中的默认行为。默认情况下，调用

```cpp
quiz[i]->display();
```

总是调用 `Question::display`，因为 `quiz[i]` 的类型是 `Question*`。

然而，在这种情况下，你真正想要确定 `quiz[i]` 所指向对象的实际类型（它可以是 `Question` 或 `ChoiceQuestion` 对象），然后调用适当的函数。在 C++ 中，必须提醒编译器该函数调用需要先进行适当的函数选择，而循环的每次迭代可能选择不同的函数。为此，使用 `virtual` 保留字：

```cpp
class Question
{
public:
    Question();
    void set_text(string question_text);
    void set_answer(string correct_response);
    virtual bool check_answer(string response) const;
    virtual void display() const;
private:
    ...
};
```

`virtual` 保留字必须在 *基类* 中使用。派生类中所有具有相同名称和参数变量类型的函数随后都会自动成为虚函数。不过，为派生类函数也提供 `virtual` 保留字被认为是良好的风格。

```cpp
class ChoiceQuestion : public Question
{
public:
    ChoiceQuestion();
    void add_choice(string choice, bool correct);
    virtual void display() const;
private:
    ...
};
```

在函数定义中不提供保留字 virtual：

```cpp
void Question::display() const // No virtual reserved word
{
    cout << text << endl;
}
```

> 当调用虚函数时，会调用属于隐式参数实际类型的版本。

每当调用虚函数时，编译器会在运行时确定特定调用中隐式参数的类型。然后调用适合该对象的函数。例如，当 display 函数被声明为虚函数时，调用

```cpp
quiz[i]->display();
```

总是调用属于 `quiz[i]` 所指向对象实际类型的函数——要么是 `Question::display`，要么是 `ChoiceQuestion::display`。

