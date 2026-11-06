
**提示**

通过将初始化列表与构造函数关联，你可以让不同的构造函数使用不同的初始化器。你不必以相同方式为所有构造函数初始化数据。

## 访问基类构造函数

你可能已经注意到，成员初始化采用的格式类似于初始化继承构造函数的方式。看看下面的代码如何调用基类构造函数：

```cpp
class MusicInfo {
public:
  int PhoneNumber;
  MusicInfo(int Phone) : PhoneNumber(Phone) {}
};

class MySharona : public MusicInfo {
protected:
  int OneHitWonders;
  int NumberRecordings;
public:
  MySharona(int Records) : OneHitWonders(1),
    NumberRecordings(Records),
    MusicInfo(8675309) {}
};
```

在 MySharona 类中，属性被初始化，基类构造函数被调用，所有这些都在初始化过程中完成。对基类构造函数的调用是这一部分：

```cpp
MusicInfo(8675309)
```

但请注意，代码向构造函数传入了一个数字。MusicInfo 构造函数接受单个数字作为参数，并使用接收到的数字初始化 PhoneNumber 成员：

```cpp
MusicInfo(int Phone) : PhoneNumber(Phone) {}
```

因此，每当有人创建 MySharona 类的实例时，继承的 PhoneNumber 成员都会自动初始化为 8675309。因此，你可以像这样创建 MySharona 的实例：

```cpp
MySharona CD(20);
```

这个实例一开始的成员值为 OneHitWonders = 1、NumberRecordings = 20 和 PhoneNumber = 8675309。用户唯一能指定的是 NumberRecordings 成员。另外两个成员由类自动设置。

但是，你不必这样做。也许你希望这个类的用户在创建实例时能够指定 PhoneNumber。下面是一个为你实现这一点的修改形式：

```cpp
class MusicInfo {
public:
    int PhoneNumber;
    MusicInfo(int Phone) : PhoneNumber(Phone) {}
};

class MySharona : public MusicInfo {
protected:
    int OneHitWonders;
    int NumberRecordings;
public:
    MySharona(int Records, int Phone) : OneHitWonders(1),
        NumberRecordings(Records), MusicInfo(Phone) {}
};
```

仔细看看区别：MySharona 类现在有两个参数。第二个是一个整数，通过这一部分传入基类：

```cpp
MusicInfo(Phone)
```

因此，要使用这个类，你可能会这样做：

```cpp
MySharona CD(20, 5551212);
```

这段代码创建了一个 MySharona 实例，成员初始化为 OneHitWonders = 1、NumberRecordings = 20 和 PhoneNumber = 5551212。

## 重载构造函数

如果你有重载的构造函数，就可以使用不同的初始化集合。再看看对 Constructor02 示例最终版本的又一处修改：

```cpp
class MySharona : public MusicInfo {
protected:
    int OneHitWonders;
    int NumberRecordings;
public:
    MySharona(int Records, int Phone) : MusicInfo(Phone),
        OneHitWonders(1), NumberRecordings(Records) {}

    MySharona(int Records) : MusicInfo(8675309),
        OneHitWonders(1), NumberRecordings(Records) {}
};
```

这个类结合前两个版本，拥有两个构造函数，所以现在你可以使用其中任意一个构造函数。例如，你可以创建两个变量，各自使用不同的构造函数：

```cpp
MySharona CD(20, 5551212);
MySharona OldCD(30);
cout << CD.PhoneNumber << endl;
cout << OldCD.PhoneNumber << endl;
```

运行这些 `cout` 行时，它们的 `PhoneNumber` 成员具有不同的值。第一个传入一个特定值；第二个接受一个默认值：

```text
5551212
8675309
```

你应该先初始化基类的值。否则，编译器在编译应用程序时很可能会显示警告消息。

### 使用默认值

如果不同构造函数之间唯一真正的区别在于用户是否提供一个值（如上一个示例中的情况），你可以使用稍微更好的方法。构造函数（实际上 C++ 中的任何函数）都可以有默认值。`Constructor03` 示例通过使用默认值缩短了前面的示例。结果相同：

```cpp
class MySharona : public MusicInfo {
protected:
    int OneHitWonders;
    int NumberRecordings;
public:
    MySharona(int Records, int Phone=8675309) :
        MusicInfo(Phone), OneHitWonders(1),
        NumberRecordings(Records) {}
};
```

![](img/128ab511de4e7360e167e3b15cdd5dd0_567_0.png)

在上面的代码中，构造函数的第二个参数后面有一个等号和一个数字，这意味着该类的用户不必指定这个参数。如果未提供该参数，它会自动获得值 8675309。

![](img/128ab511de4e7360e167e3b15cdd5dd0_567_1.png)

在构造函数或任何其他函数中，你可以拥有任意多个默认参数，但规则是默认参数必须放在末尾。一旦有了一个默认参数，后面所有参数都必须有默认值。因此，下面这种代码是不允许的：

```cpp
MySharona(int Records = 6, int Phone) {
    MusicInfo(Phone), OneHitWonders(1),
    NumberRecordings(Records) {}
}
```

这一禁止规定有一个实际原因：当用户调用构造函数（通过创建 MySharona 类型的变量）时，无法只省略第一个参数而只提供第二个参数。这是不可能的，除非 C++ 允许空参数后跟逗号，例如 MySharona(,8675309)。重载的构造函数（以及其他函数）还必须通过非可选参数来区分。否则，编译器无法判断你是想使用某个函数，还是想在省略某些参数的情况下使用另一个函数。

## 添加默认构造函数

默认构造函数是不接受任何参数的构造函数——当你没有创建任何构造函数时，编译器通常会创建它。你可以通过以下两种方式之一让类拥有默认构造函数：编写它，或者让编译器隐式地为你构建一个。每个缺少构造函数的类都会有一个由编译器创建的默认构造函数。

你以前可能见过默认构造函数。这个类没有构造函数，因此编译器会为你生成一个隐式构造函数。它的工作方式如下：

```cpp
class Simple {
public:
    int x,y;
    void Write() {
        cout << x << " " << y << endl;
    }
};
```

当然，前面的类做不了多少事情。它等同于下面这个：

```cpp
class Simple {
public:
    int x,y;
    void Write() {
        cout << x << " " << y << endl;
    }

    Simple() {}
};
```

然而，认识到默认构造函数的存在很重要。而且你需要意识到编译器何时不会自动创建构造函数，因为你可能会遇到一些问题。看看这个类的修改版本（见 Constructor04 示例）：

```cpp
class Simple {
public:
    int x,y;
    void Write() {
        cout << x << " " << y << endl;
    }

    Simple(int startx) { x = startx; }
};
```

这个类包含一个带参数的构造函数。添加这个构造函数后，该类就不再从编译器获得隐式默认构造函数。向 main() 中添加这样一行：

```cpp
Simple inst;
```

会导致编译器生成类似这样的错误消息：

```text
In function 'int main()'
  error: no matching function for call to 'Simple::Simple()'
  note: candidate: Simple::Simple(int)
  note:   candidate expects 1 argument, 0 provided
  note: candidate: constexpr Simple::Simple(const Simple&)
  note:   candidate expects 1 argument, 0 provided
  note: candidate: constexpr Simple::Simple(Simple&&)
  note:   candidate expects 1 argument, 0 provided
```

如果你移除添加的构造函数，这个错误就会消失！因此，当你没有提供任何构造函数时，编译器会为你提供一个隐式默认构造函数。

