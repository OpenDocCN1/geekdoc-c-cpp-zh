
```cpp
int main()
{
   string response;
   cout << boolalpha; // Show Boolean values as true, false

   Question q1;
   q1.set_text("Who was the inventor of C++?");
   q1.set_answer("Bjarne Stroustrup");

   q1.display();
   cout << "Your answer: ";
   getline(cin, response);
   cout << q1.check_answer(response) << endl;

   return 0;
}
```

## 程序运行

```text
Who was the inventor of C++?
Your answer: Bjarne Stroustrup
true
```

![](img/23fb3582e93ebc95909e1de029c3d388_473_0.png)

1. 考虑类Manager和Employee。哪个应该是基类，哪个应该是派生类？
2. 类BankAccount、CheckingAccount和SavingsAccount之间的继承关系是什么？
3. 考虑函数`do_something(istream& stream)`。列出图2中所有其对象可以传递给该函数的流类。
4. 考虑函数`do_something(Car& c)`。列出图1中所有其对象不能传递给该函数的车辆类。
5. 类Quiz应该继承自类Question吗？为什么？

**动手练习** 现在你可以尝试本章末尾的这些练习：R10.1、R10.2、R10.5。

## 10.2 实现派生类

在C++中，你通过指定派生类与基类的不同之处来从基类形成派生类。你定义派生类新增的成员函数。派生类继承基类的所有成员函数，但如果继承的行为不合适，你可以更改实现。

派生类自动继承基类的所有数据成员。你只需定义新增的数据成员。

以下是派生类定义的语法：

```cpp
class ChoiceQuestion : public Question
{
public:
   New and changed member functions
private:
   Additional data members
};
```

*就像加长豪华轿车的制造商，从普通汽车开始并加以改装，程序员通过修改另一个类来生成派生类。*

![](img/23fb3582e93ebc95909e1de029c3d388_474_0.png)

符号`:`表示继承。保留字`public`是出于技术原因所必需的（参见第449页的常见错误10.1）。

`ChoiceQuestion`对象与`Question`对象在三个方面有所不同：

- 它的对象存储答案的各种选项。
- 有一个用于添加另一个选项的成员函数。
- `ChoiceQuestion`类的display函数显示这些选项，以便答题者可以选择其中一个。

当`ChoiceQuestion`类继承自`Question`类时，它只需明确列出这三个不同之处：

```cpp
class ChoiceQuestion : public Question
{
public:
    ChoiceQuestion();
    void add_choice(string choice, bool correct);
    void display() const;
private:
    vector<string> choices;
};
```

图4显示了`ChoiceQuestion`对象的布局。它从`Question`基对象继承text和answer数据成员，并添加了一个额外的数据成员：choices向量。

`add_choice`函数是`ChoiceQuestion`类特有的。你只能将其应用于`ChoiceQuestion`对象，而不能用于一般的`Question`对象。然而，`display`函数是对基类中已有函数的重新定义，以考虑派生类的特殊需求。我们说派生类**覆盖**了该函数。你将在10.3节中看到具体方式。

在`ChoiceQuestion`类定义中，你只需指定新的成员函数和数据成员。`Question`类的所有其他成员函数和数据成员都会被`ChoiceQuestion`类自动继承。例如，每个`ChoiceQuestion`对象仍然具有text和answer数据成员，以及`set_text`、`set_answer`和`check_answer`成员函数。

> 派生类可以通过提供新的实现来覆盖基类函数。

> 派生类继承所有数据成员以及它未覆盖的所有函数。

![](img/23fb3582e93ebc95909e1de029c3d388_474_1.png)

**图4** 派生类对象的数据布局

在驾驶和加油方面，其他汽车也是如此。它们只是有更好的燃油效率。一个带有数据成员的`Car`类

```cpp
double miles_per_gallon;
```

就完全足够了。

# 专题10.1

![](img/23fb3582e93ebc95909e1de029c3d388_478_0.png)

## 调用基类构造函数

考虑构造派生类对象的过程。派生类构造函数只能初始化派生类的数据成员。但基类数据成员也需要被初始化。除非你另有指定，否则基类数据成员将使用基类的默认构造函数进行初始化。

> 除非另有指定，否则基类数据成员将使用默认构造函数进行初始化。

为了指定另一个构造函数，你使用初始化列表，如专题9.1中所述。在初始化列表中指定基类的名称和构造参数。例如，假设Question基类有一个用于设置问题文本的构造函数。下面是一个派生类构造函数如何调用该基类构造函数：

```cpp
ChoiceQuestion::ChoiceQuestion(string question_text)
    : Question(question_text)
{
}
```

派生类构造函数在执行{ }内的代码之前调用基类构造函数。

> 派生类的构造函数可以向基类构造函数提供参数。

在我们的示例程序中，我们使用了基类的默认构造函数。但是，如果基类没有默认构造函数，你必须使用初始化列表语法。

## 语法10.2 — 带基类初始化器的构造函数

![](img/23fb3582e93ebc95909e1de029c3d388_478_1.png)

## 10.3 覆盖成员函数

派生类继承基类的成员函数。如果你对继承的成员函数的行为不满意，可以通过在派生类中指定新的实现来覆盖它。

> 派生类可以从基类继承函数，或者通过提供另一个实现来覆盖它。

考虑ChoiceQuestion类的display函数。它需要覆盖基类的display函数，以显示答案的选项。具体来说，派生类的函数需要

- 显示问题文本。
- 显示答案选项。

第二部分很容易，因为答案选项是派生类的一个数据成员。

```cpp
void ChoiceQuestion::display() const
{
   // Display the question text
   ...
   // Display the answer choices
   for (int i = 0; i < choices.size(); i++)
   {
      cout << i + 1 << ": " << choices[i] << endl;
   }
}
```

但是如何获得问题文本呢？你不能直接访问基类的text成员，因为它是私有的。相反，你可以调用基类的display函数。

```cpp
void ChoiceQuestion::display() const
{
   // Display the question text
   display(); // Invokes implicit parameter.display()
   // Display the answer choices
   ...
}
```

然而，这并不完全有效。因为`ChoiceQuestion::display`的隐式参数类型是`ChoiceQuestion`，并且在`ChoiceQuestion`类中有一个名为`display`的函数，所以该函数将被调用——但这正是你当前正在编写的函数！该函数会反复调用自身。

为了显示问题文本，你必须更具体地指定要调用哪个名为`display`的函数。你需要`Question::display`：

```cpp
void ChoiceQuestion::display() const
{
   // Display the question text
   Question::display(); // OK
   // Display the answer choices
   ...
}
```

> 使用BaseClass::function记号来显式调用基类函数。

当你覆盖一个函数时，通常希望*扩展*基类版本的功能。因此，你通常需要在扩展之前调用基类版本。要调用它，你需要使用`BaseClass::function`记号。但是，你没有义务调用基类函数。偶尔，派生类会覆盖基类函数并指定完全不同的功能。

下面是一个完整程序，它显示一个普通的Question对象和一个ChoiceQuestion对象。（你已经见过的Question类定义放在question.h中，实现在question.cpp中。）这个例子展示了如何使用继承从基类形成一个更专门的类。
