
When assigning a value with `*number = 3`, we are indirectly modifying the variable `number` to which the pointer points.

### Pointers are used

- to allocate dynamic memory at run time.
- pass parameters to functions by reference
- access to text strings
- indirectly access to a variable and be able to change it at runtime.

## 26.- Dynamic memory

In C we can reserve memory dynamically at run time.

In practice there are two types of memory: static memory managed by the compiler and dynamic memory managed by the programmer.

When defining variables, the compiler assigns them the necessary space depending on the type of the variable.

Depending on the scope where the variable is defined, the compiler allocates memory in the stack for local variables and function parameters.

For global variables, the compiler allocates the memory of the variables in a separate data segment.

The programmer can allocate memory dynamically at run time with the `malloc` function to which the number of bytes of the memory to be reserved is passed.

The reserved memory is created in a data segment `HEAP` used only for dynamic memory.

The `malloc` function returns a pointer to the reserved memory area.

E.g.

```c
int *p = (int *) malloc (200);
```

The `malloc` function reserves 200 bytes of memory and returns an untyped pointer to the reserved zone.

An explicit casting is done to indicate that there are integers in the memory area.

The pointer `p` points to the reserved area with `malloc`.

The dynamic allocation of memory will allow us to manage quantities of data at the moment the program is executed and not at the moment of compilation.

In the previous example, if the size of an integer is 2 bytes, memory will be reserved for 100 integers.

The previous case can also be defined in the form

```c
int *p = (int *) malloc (100 * sizeof (int));
```

It should be noted that the memory reserved with `malloc` is controlled by the programmer, not the compiler, and it is he who must release it when he does not use it.

The `free` function must be used to free the dynamically allocated memory.

E.g.

```c
free (p);
```

## 6.1.2 立方根

### 知识点一 立方根的概念及性质

一般地，如果一个数的立方等于$a$，那么这个数叫做$a$的立方根或三次方根。

即：如果$x^3=a$，那么$x$叫做$a$的立方根。

求一个数的立方根的运算，叫做开立方。

开立方与立方互为逆运算。

| 数的名称 | 正数 | 负数 | 0 |
| --- | --- | --- | --- |
| 平方根 | 有两个互为相反数 | 没有平方根 | 0 |
| 立方根 | 有一个，是正数 | 有一个，是负数 | 0 |

说明：任何数都有立方根，且只有一个立方根。

### 知识点二 立方根的表示方法

一个数$a$的立方根，用符号“$\sqrt[3]{a}$”表示，读作“三次根号$a$”，其中$a$是被开方数，3是根指数。

A function can be defined in the form

### Return name (parameters)

`Return` is the value that will return the function and can be a data type (`int`, `float` ...) or `void` that is used to indicate that no value returns.

`Name` is the identifier of the function

`Parameters` is a separate list with commas of variables that we will pass to the function.

E.g.

`float CalculateVat (float price, float vat)`

### Parameter by value

The most common way to pass parameters to a function is to pass them by value.

Constants or variables are passed that will not change value in the execution of the function.

```c
float CalculateVAT (float price, float vat)
{
    return price * vat/100;
}

int main()
{
    float vat;

    vat = CalculateVAT(1000, 21);
}
```

### Parameters by reference

If we want a parameter of a function to be modified within the function and return the modified value, the parameter can be used by reference.

In this case, instead of passing the value, a pointer is passed

E.g

```c
float CalculateVAT (float price, float vat, float *pvp)
{
    float pvat;

    pvat = price *  vat / 100;
    * pvp = price + pvat;
    return pvat;
}

int main ()
{
    float vat, pvp;

    vat = CalculateVAT (1000, 21, &pvp);
}
```

This type of parameter pass is usually used when more than one value must be returned in the function.

## 28.- Data structures

Sometimes we have information regarding an entity that we want to have grouped.

For example, if we want to have data of age, weight, height ... on a person instead of have a variable for each attribute we could have it grouped in a data structure.

In C we can group variables in a `struct`

Example

```c
struct person
{
    int age;
    int weight;
    int height;
};
```

In this way we can define variable of type `person`, E.g

```c
struct person peter;
```

And access its attributes through the operator.

E.g

```c
peter.height = 175;
peter.age = 38;
```

### Pointers to structures

We can define a pointer to a structure of the form

```c
struct person *p;
```

### 用 & 符号给指针赋值

```c
p = &peter;
```

通过 `->` 符号访问结构体的字段。

```c
p -> height = 180;
```

指向结构体的指针通常用于按引用传递结构体作为参数。

## 关于作者

我叫 Enrique Vicente，是一名 IT 工程师。

我在不同技术领域开发程序方面已经有多年的经验。

我是工业控制系统和工业工厂自动化方面的专家。

我精通多种编程语言，如 C、C++、C#、Visual Basic、SQL、JavaScript、PHP 等。

我对计算机科学和信息技术充满热情，也希望激发更多人对这一领域的热情。

在我的博客 `https://evginformatica.blogspot.com` 上，你可以找到关于编程的在线课程、教程和电子书。
