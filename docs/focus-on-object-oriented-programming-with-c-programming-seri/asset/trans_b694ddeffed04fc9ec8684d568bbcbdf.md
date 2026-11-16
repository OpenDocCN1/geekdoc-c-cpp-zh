

注意：如果成员函数重载了加法运算符，表达式：

```
c = a + b;
```

在语义上等价于表达式：

```
c = a.operator+(b);
```

## 重载算术赋值运算符

该运算符将赋值和加法合并在一个步骤中。我们将使用此运算符将一个 `Distance` 对象加到第二个 `Distance` 对象上，结果保留在第一个对象中。这与之前提供了重载 `+` 运算符的 `Distance` 程序类似，只是有一个细微的差别。

```
void Distance::operator+=(Distance d) {
    feet += d.feet;
    inches += d.inches;
    if (inches > 12.0) {
        inches -= 12.0;
        ++feet;
    }
}
```

此版本的重载 `+` 运算符返回一个 `Distance` 对象，而在这里我们不返回任何内容。在之前的 `Distance` 程序中，我们创建了重载的 `+` 运算符，它允许我们将两个 `Distance` 对象相加，并使用以下方式将值赋给第三个对象：

```
d3 = d1 + d2;
```

此版本允许：

```
d1 += d2;
```

对象 `d2` 映射到 `d1`。`+=` 运算符左侧的对象是实际调用 `operator+=()` 函数的对象。因此，它可以直接访问 `feet` 和 `inches`。

注意：由于该函数直接修改 `d1`，将 `d2` 加入其中，因此无需返回值。

注意：如果您希望在更复杂的表达式中使用此运算符，例如：

```
d3 = d1 += d2;
```

您将需要返回一个 `Distance` 对象。可以通过以类似以下语句结束 `operator+=()` 函数来实现：

```
return Distance(feet, inches);
```

我们将不得不将返回值更改为 `Distance` 对象，而不是返回 `void`。这将创建一个无名对象，用值对其进行初始化，并返回它。

## 选择友元函数或成员函数

在许多情况下，使用友元函数或成员函数重载运算符时，您会得到等效的结果。友元函数只是包含一个额外的参数。友元函数必须将两个对象都传递给它，而成员函数只需要一个参数。但是，有时友元函数太方便了，无法避免。一个例子是使用友元来增加重载运算符的通用性。

例如，下面的程序显示了在不使用友元时重载运算符的局限性：

```
#include <iostream.h>

class Distance {
   private:
      int feet;
      float inches;

   public:
      Distance() {       // default constructor
         feet = 0;
         inches = 0.0;
      }
      Distance(float ffeet) {   // conversion constructor
         feet = int(ffeet);   // feet is integer part
         inches = 12 * (ffeet - feet); // inches is what's left
      }
      Distance(int ft, float in) {
         feet = ft;
         inches = in;
      }
      void showdist() {
         cout << feet << "\'-" << inches << "\"\n";
      }
      Distance operator+(Distance d);
};

Distance Distance::operator+(Distance d) {
   int ft = feet + d.feet;
   float in = inches + d.inches;
   if (in >= 12.0) {
      in -= 12.0;
      ++ft;
   }
   return Distance(ft, in);
}

int main() {
    Distance d1 = 2.5;
    Distance d2 = 1.25;
    Distance d3;

    cout << "d1 = " << d1.showdist();
    cout << "d2 = " << d2.showdist();

    d3 = d1 + 10.0;
    cout << "d3 = " << d3.showdist();

    d3 = 10.0 + d1;
    cout << "d3 = " << d3.showdist();

    return 0;
}
```

请注意，行：

```
d3 = 10.0 + d1;
```

会产生编译器错误。为什么？

在此程序中，+ 运算符被重载以添加两个类型为 Distance 的对象。还有一个单参数构造函数，它将类型为 float（表示英尺或英尺的小数部分）的值转换为 Distance 值。也就是说，将 10.25 英尺转换为 10 英尺和 3 英寸。当存在这样的构造函数时，您可以在 main() 中做出这样的语句：

```
d3 = d1 + 10.0;
```

重载的 + 运算符在其左侧和右侧都在查找类型为 Distance 的对象。但是，如果右侧的参数是 float 类型，编译器将使用单参数构造函数将 float 转换为 Distance 值，然后执行加法。

但是，为什么这行不通？

```
d3 = 10.0 + d1;
```

因为重载的 + 运算符所属的对象必须是运算符左侧的变量。当我们在那里放置不同类型的变量或常量时，就没有重载的 + 运算符可以作为其成员的对象，因此也没有构造函数将类型 `float` 转换为类型 `Distance`。编译器根本无法处理这种情况。

友元函数可以允许我们编写在运算符左侧具有非成员数据类型的语句。因此，我们可以将 `Distance` 类中的声明更改为：

```
friend Distance operator+(Distance, Distance);
```

我们现在将重新定义 `operator+()` 函数如下：

```
Distance operator+(Distance d1, Distance d2) {
    int ft = d1.feet + d2.feet;
    float in = d1.inches + d2.inches;
    if (in >= 12.0) {
        in -= 12.0;
        ++ft;
    }
    return Distance(ft, in);
}
```

现在我们可以在 `main()` 中说以下内容，而不会出现编译器错误消息：

```
d3 = d1 + 10.0;
d3 = 10.0 + d1;
```

请注意，虽然重载的 + 运算符作为成员函数时只接受一个参数，但作为友元函数时它接受两个参数。在成员函数中，+ 操作的一个对象是它所属的对象，第二个对象是参数。在友元中，两个对象都必须是参数。

友元函数对一元运算符有一个参数，对二元运算符有两个参数，而成员函数对一元运算符有零个参数，对二元运算符有一个参数。这是因为成员函数自动处理一个变量，即它被调用的对象。

## 使用 + 运算符连接字符串

请考虑以下 `String` 类：

```
const int SIZE = 100;
#include <iostream>
#include <string.h>
using namespace std;
class String {
private:
    char buf[SIZE];
public:
    String() { buf[0] = '\0'; }
    String(char s[]) { strcpy(buf, s); }
    void display() { cout << buf; }
    String operator+(String s);
};
String String::operator+(String s) {
    if (strlen(buf) + strlen(s.buf) < SIZE) {
        String temp;
        strcpy(temp.buf, buf);
        strcat(temp.buf, s.buf);
        return temp;
    }
    else
        return String(); // returns NULL String
}
int main() {
    String s1 = "Hello ", s2 = "world! ", s3;
    s3 = s1 + s2;
    s3.display();
    return 0;
}
输出：
Hello world!
```

+ 运算符接受一个类型为 `String` 的参数，并返回一个类型为 `String` 的对象。

请注意，使用 `Counter` 和 `Distance` 类时，我们能够使用以下语句简化 `operator+()` 函数：

```
return Counter(count);
```

但是，在这里我们不能使用：

```
return String(String);
```

来创建一个无名的临时 `String`，因为我们需要在多个步骤中访问临时 `String`。我们必须小心不要溢出 `String` 类中使用的固定长度字符串。我们必须检查两个字符串的组合长度不会超过最大字符串长度。如果超过，将发生溢出错误。

另请注意，您可以将两个重载的 + 运算符函数放在同一个程序中：

- `String` 对象的 + 运算符
- `Distance` 对象的 + 运算符

C++ 仍然知道如何为每个上下文解释 + 运算符。编译器将根据操作数的类型（`Distance` 或 `String`）选择正确的函数来执行“加法”。

## 重载比较 == 运算符

我们还可以探索使用重载的关系运算符来创建比较运算符 ==，以便与我们的 String 类一起用于比较两个 String 对象。如果 String 对象相同，该函数返回 true；如果不同，则返回 false。

```
#include <iostream.h>
#include <iomanip.h>
#include <string.h>

const int SIZE = 100;

using namespace std;

class String {
    private:
        char buf[SIZE];
    public:
        String() { buf[0] = '\0'; }
        String(char s[]) { strcpy(buf, s); }
        void getString() { cin.get(buf, SIZE); }
        void display() { cout << buf; }
        String operator+(String s);
        int operator==(String s);
};

String String::operator+(String s) {
    if (strlen(buf) + strlen(s.buf) < SIZE) {
        String temp;
        strcpy(temp.buf, buf);
        strcat(temp.buf, s.buf);
        return temp;
    }
    else
        return String(); // returns NULL String
}

int String::operator==(String s) {
    return !strcmp(buf, s.buf);
}

int main() {
    String s1, s2 = "YES";
    cout << "Enter YES / NO: ";
    s1.getString();
    if (s2 == s1)
        cout << "You typed YES." << endl;
    return 0;
}

