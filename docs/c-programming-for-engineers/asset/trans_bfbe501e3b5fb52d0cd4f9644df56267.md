

## 13.1. 结构体（Structs）：定义自定义数据类型

### 13.1.3 结构体指针

指针也可以指向结构体和联合体，允许对复杂数据结构进行动态分配和操作。声明结构体指针非常简单：

```c
struct Person *ptr;
```

要通过指针访问结构体成员，我们可以使用箭头运算符 (->) 或者通过解引用：

```c
ptr->age = 26;
(*ptr).age = 26;
```

在处理包含指针的结构体（例如链表）时，这个箭头运算符特别有用。
示例代码如下：

```c
#include <stdio.h>

struct Person {
    char name[18];
    int age;
    float height;
};

int main() {
```

// 声明并初始化结构体变量
struct Person person1 = {"Sarah", 20, 1.65f};
struct Person person2 = {"Adam", 25, 1.8f};

// 声明指向结构体的指针
struct Person *ptr;

// 将结构体变量的地址赋值给指针
ptr = &person1;

// 使用箭头表示法访问结构体成员
printf("Name: %s\n", ptr->name);
printf("Age: %d\n", ptr->age);
printf("Height: %f\n", ptr->height);

// 将指针指向另一个结构体
ptr = &person2;

// 使用解引用访问结构体成员
printf("Name: %s\n", (*ptr).name);
printf("Age: %d\n", (*ptr).age);
printf("Height: %f\n", (*ptr).height);
```

# 第 13 章  结构化数据

202

![](img/33fb6b7acbb6df48a3c9564e97117da6_213_0.png)

图 13.2：指向结构体的指针

```c
// 使用箭头表示法修改结构体成员
ptr->age = 26;
```

return 0;
}
```

在这个示例中，我们声明了 `ptr`，一个指向结构体的指针。然后我们将 `ptr` 设置指向第一个结构体，通过 `ptr->member` 语法访问结构体成员。接下来，我们将 `ptr` 指向另一个结构体，使用点操作符访问成员。最后，我们使用箭头运算符来修改结构体成员。

## 13.1.4 嵌套结构体

结构体可以嵌套在其他结构体中以表示复杂的数据结构。例如：

```c
struct Address {
    char street[50];
    char city[30];
};

struct Person {
    char name[10];
    int age;
    float height;
    struct Address address;
};
```

在这里，`Person` 结构体包含一个嵌套的 `Address` 结构体，用于表示人的地址。

## 13.1.5 向函数传递结构体

结构体可以通过值传递或引用传递传递给函数。例如：

```c
void printPerson(struct Person p) {
    printf("Name: %s, Age: %d, Height: %f\n", p.name, p.age, p.height);
}

// 按值传递
struct Person p = {"Adam", 25, 1.8};
printPerson(p);
```

## 13.1.6 从函数返回结构体

函数也可以返回结构体。例如：

```c
struct Person createPerson(char name[], int age) {
    struct Person p;
    strcpy(p.name, name);
    p.age = age;
    return p;
}
```

此函数创建并返回一个带有指定名称和年龄的 `Person` 结构体。

## 12.2 联合体（Unions）：一种特殊的结构体

在 C 语言编程中，联合体提供了一种创建唯一类型结构的方法，其中所有成员共享同一块内存。

联合体提供了一种创建唯一类型结构的方法，其中所有成员共享相同的内存。要声明联合体，使用 `union` 关键字后跟名称。例如：

```c
union myList {
    char c;
    int i;
    double d;
};
```

联合体与结构体的区别在于，联合体同一时间只有一个成员是激活的，而结构体的每个成员都有自己的内存空间。联合体的大小由其最大成员的大小决定。

联合体通常用于节省内存。下面是比较结构体和联合体的用法：

```c
#include <stdio.h>

// 使用结构体表示不同数据类型
struct myststruct {
    char c;
    int i;
    double d;
};

// 使用联合体表示不同数据类型
union myunion {
    char c;
    int i;
    double d;
};

int main() {
    union myunion u;
    struct myststruct s;

    printf("结构体的大小: %d\n", sizeof(s));
    printf("联合体的大小: %d\n", sizeof(u));

    u.c = 'a';
    printf("值: %c\n", u.c);
}
```

## 13.3 typedef：简化声明

`typedef` 关键字用于为现有数据类型创建别名，这可以使代码更具读性且易于维护。对于结构体和联合体等复杂类型特别有用。

例如，与其每次都写 `struct Person`，你可以定义一个 `typedef` `Person`。

```c
typedef struct {
    int age;
    float height;
} Person;

Person p1; // 现在可以使用 Person 代替 struct Person
```

`typedef` 也可以用于指针和数组：

```c
typedef int* intPtr;
typedef int intArray[10];
```

## 13.4 枚举（Enums）：提高程序可读性

枚举（enums）是定义命名整数常量的方法。与使用魔数相比，这使得代码更具读性，因为名称提供了清晰的上下文。

要定义枚举，使用 `enum` 关键字后跟名称：

```c
enum Day {
    SUNDAY,
    MONDAY,
    TUESDAY,
    WEDNESDAY,
    // ... (省略)
};
```

默认情况下，第一个常量为 0，随后的每个常量增加 1。你也可以分配特定的值：

```c
enum Status {
    LOW = 1,
    MEDIUM = 2,
    HIGH = 10
};
```

配合 `typedef` 使用枚举允许你在声明变量时避免使用 `enum` 关键字：

```c
typedef enum { SUNDAY, MONDAY, TUESDAY } Day;

Day today = MONDAY;
```

