

## Friends

面向对象编程的主要恩赐之一是将数据封装在类中。我们已经见过许多这种数据隐藏概念的示例，并考虑过其降低维护成本和更易于调试的优点。

像生活和编程中的许多规则一样，数据隐藏的规则也可以被打破。在 C++ 中，你可以通过使用友元（friends）来打破封装的规则，尽管这样做对程序的健康存在一定风险。友元机制允许类的非成员访问类的私有成员。

C++ 类可以声明两种友元：

- 整个类可以是另一个类的友元。
- 单个函数可以被声明为友元。

注意：如果友元在其他语言中有对应物，那就是 `goto` 语句。像 `goto` 一样，友元允许你打破旨在帮助你编写可靠代码的规则。不要将以下内容解读为对友元的认可。顶尖 C++ 程序员除非万不得已，否则避免使用友元。不言而喻，C++ 中使用友元函数是有争议的。

## 友元类

一个类可以将另一个类声明为其友元。第一个类（声明友元的类）授予另一个类（友元）访问第一个类所有私有成员的权限。请注意，公有成员始终可访问，因此你不需要将一个类声明为友元来让它访问公有成员。

通常，当两个不相关的类需要访问某个类的私有部分时，会使用友元类。例如：

```
class Alpha {
private:
    double value;
public:
    Alpha() { value = 3.14159; }
};
```

现在，假设你声明另一个类，该类包含一个 Alpha 类型的对象作为数据成员：

```
class Beta {
private:
    Alpha anObject;
public:
    void showValue() {
        cout << anObject.value;
    }
};
```

类型为 Alpha 的成员 anObject 对 Beta 来说是私有的。成员函数 showValue() 尝试显示 anObject 的 value。然而，该声明无法编译，因为 value 是 Alpha 的私有成员，只有 Alpha 中的成员函数才能访问 value。

解决方案是将 Beta 类声明为 Alpha 类的友元。这样，Beta 类的对象就可以访问 value 以及 Alpha 类的任何其他私有成员。但是，两个类之外的语句仍然无法进入 Alpha 的受限区域。要进行此更改，我们在需要被访问的类内部使用 `friend` 关键字。例如：

```
class Alpha {
private:
    double value;
public:
    Alpha() { value = 3.14159; }
    friend class Beta; // Beta is a friend of Alpha
};
```

在这里，Beta 类必须访问 Alpha 类内部的私有 value 成员。因此，为了授予 Beta 类使用该私有数据的权限，Alpha 类可以将 Beta 类声明为友元。现在，Beta 可以访问 Alpha 的私有成员。

请注意，其他类和 `main()` 程序中的其他语句仍然无法使用 Alpha 的私有声明。以这种方式，你可以声明任意数量的类为友元。唯一的限制是 `friend` 关键字必须出现在类声明内部。

请注意以下几点：

- 类必须提前声明所有的友元
- 包含私有数据的类是声明另一个类为友元的类，从而授予该友元访问声明类通常隐藏成员的特殊权限。一个类永远不能将自身声明为另一个类的友元。
- 友元类可以在声明友元的类之前或之后声明。声明顺序无关紧要，但友元类通常最后声明，以便友元的内联成员函数可以引用另一个类的私有部分。

## 友元函数

友元函数与友元类类似。将函数声明为类的友元会赋予该函数访问类对象中私有成员的权限。友元函数可以是普通的 C++ 函数，也可以是类成员函数。

友元函数声明了函数与之建立友谊的类的参数，这使得友元函数可以访问类对象的私有成员。

友元函数具有与成员函数相同的访问权限，但不与宿主类的对象相关联。

宿主类控制授予其他函数友元权限，因此你始终知道谁有能力修改你的私有数据。

有时候程序设计就是无法完美运作。你不能总是把所有东西都整齐地塞进一个类中。有时，其他函数必须能够访问你类的私有元素，才能使一切和谐协调地工作。你可以将一些元素设为公有，但除非你真的希望客户端程序员修改数据，否则这是个坏主意。

```
#include <iostream>

using namespace std;
class Beta; // incomplete class declaration allows class Alpha
// to refer to class Beta

class Alpha {
private:
    char *s1;
public:
    Alpha() {
        s1 = new char(strlen("Testing")+1);
        strcpy(s1, "Testing");
    }
    friend void show(Alpha a, Beta b);
};

class Beta {
private:
    char* s2;
public:
    Beta() {
        s2 = new char(strlen("one, two, three")+1);
        strcpy(s2, "one, two, three");
    }
    friend void show(Alpha a, Beta b);
};

void show(Alpha a, Beta b) {
    cout << a.s1 << b.s2;
}

int main() {
    Alpha a;
    Beta b;
    show(a, b);
    return 0;
}
```

请注意，友元函数声明必须出现在其作为友元的类声明内部。该函数由关键字 `friend` 引导，可以出现在类的公有部分或私有部分，而不会影响其含义。

友元函数不是成员函数，因此不会隐式地将 `this` 指针作为其第一个参数传递。

友元函数不在类的作用域内，但与在 C++ 中声明的任何普通函数具有相同的作用域。然而，这些函数就像成员函数一样，可以访问类的所有访问区域。

成员函数与友元函数之间的一个重大区别在于函数如何获取它将读取或写入的对象的地址。在友元函数中，我们必须显式传递感兴趣的对象或对该对象的引用。我们将在运算符重载中看到这一点。

请注意，关键字 `friend` 出现在类内部的函数声明中，而不出现在函数定义中。只有类才能说明谁是它的友元。如果任何函数都能将自身声明为特定类的友元，那么该函数就可以在不经过类接口的情况下访问私有数据。

## 友元成员函数

一个类的成员函数可以是另一个类的友元。例如，一个类可以将另一个类的成员函数声明为友元。友元成员函数可以访问声明类的私有成员。

```
#include <iostream>

using namespace std;

class Alpha;

class Beta {
private:
    char* s2;
public:
    Beta() {
        s2 = new char(strlen("one, two, three")+1);
        strcpy(s2, "one, two, three");
    }
    void show(Alpha a);
};

class Alpha {
private:
    char *s1;
public:
    Alpha() {
        s1 = new char(strlen("Testing")+1);
        strcpy(s1, "Testing");
    }
    friend void Beta::show(Alpha a);
};

void Beta::show(Alpha a) {
    cout << a.s1 << s2;
}

int main() {
    Alpha a;
    Beta b;
    b.show(a);
    return 0;
}
```

请注意，两个类的顺序与前一个示例相反，因为声明成员函数原型的类必须在将成员函数指定为友元的类之前被声明。例如，为了让 Alpha 将 `Beta::show()` 声明为类的友元，编译器必须已经见过 Beta 的声明。

另一个区别是 `show()` 引用两个类中私有数据的方式。该成员函数只声明一个参数 Alpha a。因为 `show()` 是 Beta 类的成员，所以它可以直接访问 Beta 的所有成员。

表达式 a.s1 是允许的，因为 `show()` 是 Alpha 类的友元，而 s1 是 Alpha 类的私有数据成员。

`show()` 可以直接引用 s2，因为这个成员函数属于 Beta 类，即声明 `show()` 的同一个类。

因为 `show()` 是 Beta 类的成员函数，它现在有一个指向调用该成员函数的类对象的 `this` 指针。因此，程序必须定义一个 Beta 类的对象，然后为该对象调用 `show()`。

