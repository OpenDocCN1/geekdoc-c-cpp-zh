
```cpp
23:     }
24: TickCounter operator ++ (int)                 //Postfix Implementation
25: {
26:     return TickCounter(count++);
27: }
28: };
29:
30:int main()
31:{
32:    TickCounter obj1, obj2;
33:
34:    cout<<"The value of Obj1 = "<<obj1.getCount()<<endl;
35:    cout<<"The value of Obj2 = "<<obj2.getCount()<<endl;
36:
37:    ++obj1;
38:    obj2 = ++obj1;
39:
40:    cout<<"The value of Obj1 = "<<obj1.getCount()<<endl;
41:    cout<<"The value of Obj2 = "<<obj2.getCount()<<endl;
42:
43:    obj2 = obj1++;
44:
45:    cout<<"The value of Obj1 = "<<obj1.getCount()<<endl;
46:    cout<<"The value of Obj2 = "<<obj2.getCount()<<endl;
47:
48:    return 0;
49:}
```

在以上程序中，我们看到了重载‘++’运算符的两种不同定义。以下是以上程序的输出：

```text
The value of Obj1 = 0
The value of Obj2 = 0

The value of Obj1 = 2
The value of Obj2 = 2

The value of Obj1 = 3
The value of Obj2 = 2
```

程序的输出确认了第43行中的后缀递增操作成功工作。在输出中，obj1递增为3，但obj2在递增前被赋值为obj1的值；因此，obj2保留了值2，而obj1将其自身值递增为3。类似的方法也可以应用于递减运算符。

## 重载二元运算符

二元运算符是那些同时对两个操作数进行操作的运算符。二元运算符的一些示例包括加法（+）、乘法（*）、减法（-）和除法（/）。二元运算符可以像一元运算符一样被重载。让我们编写以下程序来重载二元加法

```cpp
1:/* Operator Overloading Example Program 5 */
2:#include <iostream.h>
3:using namespace std;
4:
5:class Time {
    int hour;
    int minutes;
    int seconds;

public:
    Time()
    {
        hour=minutes=seconds=0;
    }
    Time(int hr, int min, int sec)
    {
        hour = hr;
        minutes = min;
        seconds = sec;
    }
    int showTime ()
    {
        cout<<"The Time is: "<<hour<<":"<<minutes<<":"<<seconds<<endl;
    }
    Time operator + (Time T2)
    {
        int hr,min,sec;
        hr=min=sec=0;
        hr = hour + T2.hour;
        sec = seconds + T2.seconds;
        if (sec >= 60) {
            min = sec / 60;
            sec = sec % 60;
        }
        min += minutes + T2.minutes;
        if (min >= 60) {
            hour += (min / 60);
            min = min % 60;
        }
        return Time(hr,min,sec);
    }
};

int main()
{
    Time obj1(12,20,23);
    Time obj2(20,45,30);
    Time obj3, obj4;

    obj1.showTime();
    obj2.showTime();
    obj3.showTime();
    obj4.showTime();

    obj3 = obj1 + obj2;

    obj1.showTime();
    obj2.showTime();
    obj3.showTime();
    obj4.showTime();

62:        obj4 = obj1 + obj2 + obj3;
63:
64:        obj1.showTime();
65:        obj2.showTime();
66:        obj3.showTime();
67:        obj4.showTime();
68:
69:        return 0;
70:}
```

为了表明加法结果既可用于加法也可用于赋值，在 main() 函数中执行了加法操作。也就是说，我们在第62行中相加 obj1、obj2 和 obj3 以获得 obj4。在进一步解释之前，让我们先看看输出：

```text
The Time is:  12:20:23
The Time is:  20:45:30
The Time is:  0:0:0
The Time is:  0:0:0

The Time is:  12:20:23
The Time is:  20:45:30
The Time is:  32:5:53
The Time is:  0:0:0

The Time is:  12:20:23
The Time is:  20:45:30
The Time is:  33:5:53
The Time is:  66:11:46
```

在 Time 类中，operator+() 的声明如下：

```cpp
Time operator + (Time T2);
```

上述函数接受一个 Time 类型的参数，并返回一个 Time 类型的值。理解运算符的返回值和参数如何与对象关联非常重要。第25行中的运算符函数将两个 Time 对象相加，并返回另一个设置了结果值的 Time 对象。Time 对象以小时:分钟:秒格式包含时间，加法之后，结果也应遵循类似格式，且秒和分钟的值保持在60以下。第25行中的运算符函数接受一个 Time 对象作为参数，并返回另一个设置了结果值的 Time 对象。当编译器在第55行遇到‘+’运算符时，它会立即检查 obj1 和 obj2 是内置数据类型还是用户定义类型，然后按需继续。在本例中，发现 obj1 和 obj2 的数据类型为 Time 类，于是编译器立即在类空间中搜索该类的‘+’运算符定义。当编译器找到该定义时，它执行为实现‘+’运算符重载而编写的代码块。

在第55行中，运算符左侧的参数，即 obj1，是该运算符作为其成员的对象。运算符右侧的对象，即 obj2，作为参数提供给运算符。函数执行后，操作结果在一个匿名临时对象中返回，并存储到 obj3 中。

在运算符函数中，位于运算符左侧的对象的成员可以直接访问。因此，在本例中，我们可以在运算符函数中直接访问 obj1 的成员变量。要访问运算符右侧对象的值，我们使用参数：obj2.hour、obj2.seconds 或 obj2.minutes。如前所述，重载运算符所需的参数总是比操作数数量少一个。类似的运算逻辑应用于第63行，其中我们将三个 Time 类对象相加以获得结果值。在这种情况下，首先执行 obj2 和 obj3 之间的加法，然后执行 obj1 与作为 obj2 和 obj3 相加结果返回的匿名对象之间的另一次加法，以获得最终值。

类似地，其他二元运算符，如 -、+ 或 *，也可以被重载。让我们为 TickCounter 类重载 C++ 中的 += 运算符，如下所示：

```cpp
1:/* Operator Overloading Example Program 6 */
2:#include <iostream.h>
3:using namespace std;
4:
5:class TickCounter {
6:   int count;
7:public:
8: TickCounter()
9: {
10:       count=0;
11:   }
12:   TickCounter(int cnt)
13:   {
14:       count = cnt;
15:   }
16: int getCount ()
17: {
18:       return this->count;
19: }
20: void operator += (TickCounter obj)
21: {
22:       count = count + obj.count;
23:   }
24:};
25:
26:int main()
27:{
28:   TickCounter obj1(100);
29:   TickCounter obj2(450);
30:
31:   cout<<"The value of Obj1 = "<<obj1.getCount()<<endl;
32:   cout<<"The value of Obj2 = "<<obj2.getCount()<<endl;
33:
34:   obj1 += obj2;
35:
36:   cout<<"\nThe value of Obj1 = "<<obj1.getCount()<<endl;
37:   cout<<"The value of Obj2 = "<<obj2.getCount()<<endl;
38:
39:   return 0;
40:}
```

在以上程序中，我们在 TickCounter 类上重载了 += 运算符，以展示如何实现它来处理用户定义的类对象。当我们重载这类运算符时，只需记住我们只是将赋值运算符与加法运算符组合在一起。以下是以上程序的输出：

```text
The value of obj1 = 100
The value of obj2 = 450
The value of obj1 = 550
The value of obj2 = 450
```

现在，让我们重载 '==' 运算符来检查两个字符串对象，如下所示：

```cpp
1:/* Operator Overloading Example Program 7 */
2:#include <iostream.h>
3:#include <string.h>
4:using namespace std;
5:
6:class String {
7:    char str[500];
8:public:
9:    String()
10:    {
11:        strcpy(str, "");
12:    }
13:    String(char tmp[])
14:    {
15:        strcpy(str, tmp);
16:    }
17:    int show ()
18:    {
19:        cout<<str<<endl;
20:    }
21:    bool operator == (String target)
22:    {
23:        return (strcmp(str, target.str) == 0) ? true : false;
24:    }
25:};
26:
27:int main()
28:{
29:    String s1 = "yes";
30:    String s2 = "no";
31:    char tempstr[500];
32:
33:        cout<<"Enter 'yes' or 'no' :"<<endl;
34:        cin>>tempstr;
35:
36:        String final (tempstr);        // Create a new object using tempstr
37:
38:        if (s1 == final)
39:            cout<<"You typed 'yes'"<<endl;
40:        else if (s2 == final)
41:            cout<<"You typed 'no'"<<endl;
42:        else
43:            cout<<"Invalid Input"<<endl;
44:
45:    return 0;
46:}
```

在以上程序中，我们重载了 '==' 运算符来检查两个字符数组或字符串是否相等。一旦编译器检测到 '==' 运算符的操作数不同于内置类型，它就会立即将其链接到 string 类中的运算符成员函数，并在第38行和第40行两种情况下执行它。由于这是布尔运算，重载运算符函数的返回类型保持为 bool，根据操作是否成功返回 true 或 false。以下是以上程序的输出：

```text
Enter 'yes' or 'no' : yes
You typed 'yes'
```

