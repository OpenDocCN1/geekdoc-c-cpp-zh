

cout<<b1.volume(5,2,3)<<endl;
cout<<b1.calculate_base_area(2,3);
}

上述程序会报出各种错误，提示“int cuboid::length is private”。

权限级别有三种：private、protected 和 public。但在这里，这些级别更加重要。它们赋予我们封装的能力。通过封装，我们可以封装类的成员和方法，并将其限制在派生类中，还可以进一步扩展到更多派生类。

假设我们从 base_area 类派生另一个类，如下所示：

```
#include<iostream>
using namespace std;
class cuboid
{
 public:
 int length,breadth,height;
 int volume(int,int,int);
};
```

```
int cuboid::volume(int x,int y,int z)
{
 length=x;
 breadth=y;
 height=z;
 return length*breadth*height;
}
```

```
class base_area:public cuboid
{
 public:
 int calculate_base_area();
};
int base_area::calculate_base_area()
{
    return length*breadth;
}
```

```
class side_area:public base_area
{
    public:
    int calculate_side_area();
};
```

```
int side_area::calculate_side_area()
{
    return length*height;
}
```

```
int main()
{
    class side_area s1;
    cout<<"Volume of cuboid is: "<<s1.volume(2,3,4)<<endl;
    cout<<"Base area of cuboid is: "<<s1.calculate_base_area()<<endl;
    cout<<"Area of side wall of cuboid is: "<<s1.calculate_side_area();
}
```

输出
长方体的体积是：24
长方体的基面积是：6
长方体的侧面积是：8

在上述程序中，我们使用了 **公有** 关键字，因此基类可从派生类访问。如果我们使用 **私有** 关键字呢？

## 继承中的可访问性

考虑以下程序：

```
#include<iostream>

using namespace std;

class cuboid
{

    public:

    int length,breadth,height;

    int volume(int,int,int);

};

int cuboid::volume(int x,int y,int z)
{

    length=x;

    breadth=y;

    height=z;

    return length*breadth*height;

}

class base_area:private cuboid
{

    public:

    int calculate_base_area();

};

int base_area::calculate_base_area()
{
    return length*breadth;
}
```

```
int main()
{
    class base_area b1;

    cout<<"Volume of cuboid is: "<<b1.volume(2,3,4)<<endl;
    cout<<"Base area of cuboid is: "<<b1.calculate_base_area()<<endl;
}
```

该程序将生成错误“[Error] 'int cuboid::volume(int, int, int)' is inaccessible”。这意味着存在某些规则，类遵循这些规则。规则如下：

## 私有继承：

| 权限级别 | 私有成员 | 保护成员 | 公有成员 |
|---|---|---|---|
| 在基类中可访问 | 是 | 是 | 是 |
| 在派生类中可访问 | 否 | 是 | 是 |
| 在派生类外可访问 | 否 | 否 | 否 |

## 保护继承：

| 权限级别 | 私有成员 | 保护成员 | 公有成员 |
|---|---|---|---|
| 在基类中可访问 | 是 | 是 | 是 |
| 在派生类中可访问 | 否 | 是 | 是 |
| 在派生类外可访问 | 否 | 否 | 否 |

## 公有继承：

| 权限级别 | 私有成员 | 保护成员 | 公有成员 |
|---|---|---|---|
| 可访问性 | | | |
| 在基类中可访问 | 是 | 是 | 是 |
| 在派生类中可访问 | 否 | 是 | 是 |
| 在派生类外可访问 | 否 | 否 | 是 |

现在，你已经理解了在上述程序中，我们尝试通过 base_area 类的对象 b1 使用私有继承来访问 volume 函数，但通过私有继承，派生类外部（即 main() 函数中）不可访问公有成员。这就是编译器给出相应错误的原因。

要记住上述图表，只需记住“是”的位置。你会看到一个模式：123、122、122。

### 注意：

- 1. 类中定义的任何成员始终可被该类中声明或定义的所有函数访问
- 2. 基类的私有成员不能被继承

## 继承类型

### 单一继承

如果从一个基类派生一个类，那么形成的架构称为单一继承。

![](img/5340985153962870d4e4a3b9453b9146_205_0.png)

### 单一继承

本章使用的第一个程序是单一继承的一种类型。

### 多级继承

在上述程序中，你可以看到我们从一个基类（假设为 A）继承了一个类（假设为 B），然后又从继承类 B 继承了一个类（假设为 C）。这称为多级继承。

![](img/5340985153962870d4e4a3b9453b9146_206_0.png)

### 多级继承

本章使用的第三个程序是多级继承的一种类型。

### 层次继承

如果从单个基类派生多个类，则此继承为层次继承。

![](img/5340985153962870d4e4a3b9453b9146_206_1.png)

### 层次继承

```
#include<iostream>
using namespace std;
class cuboid
{
    public:
    int length,breadth,height;
    int volume(int,int,int);
};

int cuboid::volume(int x,int y,int z)
{
    length=x;
    breadth=y;
    height=z;
    return length*breadth*height;
}

class base_area:public cuboid
{
    public:
        int calculate_base_area();
};

int base_area::calculate_base_area()
{
    return length*breadth;
}

class side_area:public cuboid
{
    public:
        int calculate_side_area();
};

int side_area::calculate_side_area()
{
    return length*height;
}
```

```

int main()
{
    class base_area b1;
    class side_area s1;
    cout<<"Volume of cuboid is: "<<b1.volume(2,3,4)<<endl;
    cout<<"Base area of cuboid is: "<<b1.calculate_base_area()<<endl;
    cout<<"Volume of second cuboid is: "<<s1.volume(3,4,5)<<endl;
    cout<<"Area of side wall of second cuboid is: "<<s1.calculate_side_area();
}
```

输出
长方体的体积是：24
长方体的基面积是：6
第二个长方体的体积是：60
第二个长方体的侧面积是：15

在这里，我们从类 cuboid 继承了两个类 base_area 和 side_area。

### 多重继承

如果从多个基类派生一个类，那么形成的架构称为多重继承。

![](img/5340985153962870d4e4a3b9453b9146_208_0.png)

### 多重继承

这是一种惊人的继承类型；使用这种继承类型，我们可以从多个基类继承一个类。

在此，要从多个基类继承，我们使用以下语法：

```
class inherited_class: permission_level class_name,permission_level class_name
{
    //Statements
}
```

以下代码片段将消除您的所有困惑：

```
class cuboid:public base_area,public side_area
{
public:
int volume();
};
```

现在，考虑以下程序：

```
#include<iostream>
using namespace std;
class base_area
{
public:
int length,breadth;
int calculate_base_area(int,int);
};
int base_area::calculate_base_area(int p,int q)
{
length=p;
breadth=q;
return length*breadth;
}
class side_area
{
public:
    int x,z;
    int calculate_side_area(int,int);
};

int side_area::calculate_side_area(int a,int b)
{
    x=a;
    z=b;
    return x*z;
}

class cuboid:public base_area,public side_area
{
    public:
    int volume();
};

int cuboid::volume()
{
    return length*breadth*z;
}

int main()
{
    class cuboid c1;
    cout<<"Base area of cuboid is: "<<c1.calculate_base_area(3,4)<<endl;
    cout<<"Area of side wall is: "<<c1.calculate_side_area(3,5)<<endl;
    cout<<"Volume of cuboid is: "<<c1.volume()<<endl;
}
```

## 输出

长方体的基面积是：12

长方体的侧面积是：15

长方体的体积是：60

### 混合继承

两种或多种继承类型的组合称为混合继承。

![](img/5340985153962870d4e4a3b9453b9146_211_0.png)

混合继承

在以下程序中，我们混合了多重继承和单一继承。你也可以将其视为多重继承和多级继承的混合。

考虑以下程序：

```
#include<iostream>
using namespace std;
class base_area
{
public:
int length,breadth;
int calculate_base_area(int,int);
};
int base_area::calculate_base_area(int p,int q)
{

