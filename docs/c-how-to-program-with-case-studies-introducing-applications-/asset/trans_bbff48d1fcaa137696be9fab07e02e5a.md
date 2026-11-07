
- e) 使用指针 nPtr 以指针/偏移量表示法打印 numbers 的元素。
- f) 使用数组名作为指针，以指针/偏移量表示法打印 numbers 的元素。
- g) 通过对指针 nPtr 使用下标来打印 numbers 的元素。
- h) 使用数组下标表示法、以数组名作为指针的指针/偏移量表示法、nPtr 的指针下标表示法以及 nPtr 的指针/偏移量表示法引用 numbers 的元素 4。
- i) 假设 nPtr 指向数组 numbers 的起始位置，nPtr + 8 引用什么地址？该位置存储什么值？
- j) 假设 nPtr 指向 numbers[5]，nPtr − 4 引用什么地址？该位置存储的值是什么？

## 7.4

对以下每一项，编写一条执行指定任务的语句。假设已定义 float 变量 number1 和 number2，并且 number1 初始化为 7.3。

- a) 定义变量 fPtr 为指向 float 类型对象的指针。
- b) 将变量 number1 的地址赋给指针变量 fPtr。
- c) 打印 fPtr 所指向对象的值。
- d) 将 fPtr 所指向对象的值赋给变量 number2。
- e) 打印 number2 的值。
- f) 打印 number1 的地址。使用 %p 转换说明。
- g) 打印存储在 fPtr 中的地址。使用 %p 转换说明符。打印的值与 number1 的地址相同吗？

## 7.5

完成以下每一项：

- a) 为函数 exchange 编写函数头，该函数接受两个指向浮点数 x 和 y 的指针作为参数，并且不返回值。
- b) 为 (a) 部分中的函数编写函数原型。
- c) 为函数 evaluate 编写函数头，该函数返回整数，并接受整数 x 和指向函数 poly 的指针作为参数，poly 表示一个接受整数参数并返回整数的函数。
- d) 为 (c) 部分中的函数编写函数原型。

## 7.6

找出以下每个程序段中的错误。假设：

```
int *zPtr; // zPtr will reference array z
int *aPtr = NULL;
void *sPtr = NULL;
int number;
int z[5] = {1, 2, 3, 4, 5};
sPtr = z;
```

- a) ++zPtr;
- b) // use pointer to get array
  number = zPtr;
- c) // assign array element 2 to number; assume zPtr is initialized
  number = *zPtr[2];

d) // print entire array z; assume zPtr is initialized
    for (size_t i = 0; i <= 5; ++i) {
        printf("%d ", zPtr[i]);
    }
e) // assign the value pointed to by sPtr to number
    number = *sPtr;
f) ++z;

## 自测练习答案

- 7.1 a) 地址。b) 0、NULL、一个地址。c) 0。

- 7.2 a) *错误。* void 指针不能被解引用，因为无法确切知道要解引用多少字节的内存。 b) *错误。* void 类型的指针可以被赋值为其他类型的指针，并且 void 类型的指针可以赋值给其他类型的指针。

- 7.3 见下面的答案：

```
a) float numbers[SIZE] =
       {0.0, 1.1, 2.2, 3.3, 4.4, 5.5, 6.6, 7.7, 8.8, 9.9};
b) float *nPtr;
```

```
c) for (size_t i = 0; i < SIZE; ++i) {
       printf("%.1f ", numbers[i]);
   }
```

```
d) nPtr = numbers;
   nPtr = &numbers[0];
```

```
e) for (size_t i = 0; i < SIZE; ++i) {
       printf("%.1f ", *(nPtr + i));
   }
```

```
f) for (size_t i = 0; i < SIZE; ++i) {
       printf("%.1f ", *(numbers + i));
   }
```

```
g) for (size_t i = 0; i < SIZE; ++i) {
       printf("%.1f ", nPtr[i]);
   }
```

```
h) numbers[4]
   *(numbers + 4)
   nPtr[4]
   *(nPtr + 4)
```

- i) 地址是 1002500 + 8 * 4 = 1002532。值是 8.8。

- j) numbers[5] 的地址是 1002500 + 5 * 4 = 1002520。
  nPtr - 4 的地址是 1002520 - 4 * 4 = 1002504。
  该位置的值是 1.1。

- 7.4 见下面的答案：

```
a) float *fPtr;
```

- b) `fPtr = &number1;`
- c) `printf("The value of *fPtr is %f\n", *fPtr);`
- d) `number2 = *fPtr;`
- e) `printf("The value of number2 is %f\n", number2);`
- f) `printf("The address of number1 is %p\n", &number1);`
- g) `printf("The address stored in fPtr is %p\n", fPtr);`
  是的，该值相同。

- 7.5
- a) `void exchange(float *x, float *y)`
- b) `void exchange(float *x, float *y);`
- c) `int evaluate(int x, int (*poly)(int))`
- d) `int evaluate(int x, int (*poly)(int));`

- 7.6
- a) 错误：zPtr 尚未初始化。
  更正：在进行指针运算之前，用 zPtr = z; 初始化 zPtr。
- b) 错误：指针没有被解引用。
  更正：将该语句改为 number = *zPtr;
- c) 错误：zPtr[2] 不是指针，不应被解引用。
  更正：将 *zPtr[2] 改为 zPtr[2]。
- d) 错误：使用指针下标引用了数组边界之外的数组元素。
  更正：将 for 条件中的运算符 <= 改为 <。
- e) 错误：解引用 void 指针。
  更正：要解引用该指针，必须首先将其强制转换为整数指针。将该语句改为 number = *((int *) sPtr);
- f) 错误：试图用指针运算修改数组名。
  更正：使用指针变量而不是数组名来完成指针运算，或对数组名使用下标来引用特定元素。

## 练习题

- 7.7 回答以下各项：
  - a) ________ 运算符返回其操作数在内存中的位置。
  - b) ________ 运算符返回其操作数所指向对象的值。
  - c) 将非数组变量传递给函数时，为了实现按引用传递，有必要将变量的 ________ 传递给函数。

- 7.8 说明以下各项是真还是假。如果是假，请解释原因。
  - a) 指向不同数组的两个指针不能进行有意义的比较。
  - b) 因为数组名是指向数组第一个元素的指针，所以数组名可以以与指针完全相同的方式操作。

- 7.9 回答以下各项。假设整数存储在四个字节中，并且数组的起始地址位于内存位置 1002500。
  - a) 定义一个包含五个元素的 int 数组 values，并将这些元素初始化为从 2 到 10 的偶数。假设符号常量 SIZE 定义为 5。
  - b) 定义一个指针 vPtr，它指向 int 类型的对象。
  - c) 使用数组下标表示法打印数组 values 的元素。使用 for 语句，并假设已定义整数控制变量 i。
  - d) 给出两条单独的语句，将数组 values 的起始地址赋给指针变量 vPtr。
  - e) 使用指针/偏移量表示法打印数组 values 的元素。
  - f) 使用数组名作为指针的指针/偏移量表示法打印数组 values 的元素。
  - g) 通过对指向数组的指针使用下标来打印数组 values 的元素。
  - h) 使用数组下标表示法、通过数组名的指针/偏移量表示法、指针下标表示法和指针/偏移量表示法引用 values 的元素 4。
  - i) vPtr + 3 引用什么地址？该位置存储什么值？
  - j) 假设 vPtr 指向 values[4]，vPtr - 4 引用什么地址？该位置存储什么值？

## 7.10 对以下每一项，编写一条执行指定任务的语句。

假设已定义长整型变量 value1 和 value2，并且 value1 已初始化为 200000。

- a) 定义变量 lPtr 为指向 long 类型对象的指针。
- b) 将变量 value1 的地址赋给指针变量 lPtr。
- c) 打印 lPtr 所指向对象的值。
- d) 将 lPtr 所指向对象的值赋给变量 value2。
- e) 打印 value2 的值。
- f) 打印 value1 的地址。
- g) 打印存储在 lPtr 中的地址。该值与 value1 的地址相同吗？

## 7.11 完成以下每一项：

- a) 为函数 zero 编写函数头，该函数接受长整型数组参数 bigIntegers，并且不返回值。
- b) 为 (a) 部分中的函数编写函数原型。
- c) 为函数 add1AndSum 编写函数头，该函数接受整数数组参数 oneTooSmall 并返回一个整数。
- d) 为 (c) 部分中描述的函数编写函数原型。

*注意：练习 7.12–7.15 具有相当的挑战性。完成这些问题后，你应该能够轻松实现大多数流行的纸牌游戏。*

## 7.12（洗牌和发牌：发扑克牌手牌）修改图 7.16 中的程序，使发牌函数发一手五张牌的扑克牌手牌。然后编写以下附加函数：

- a) 判断该手牌是否包含一对。
- b) 判断该手牌是否包含两对。
- c) 判断该手牌是否包含三条（例如三张 J）。
- d) 判断该手牌是否包含四条（例如四张 A）。

