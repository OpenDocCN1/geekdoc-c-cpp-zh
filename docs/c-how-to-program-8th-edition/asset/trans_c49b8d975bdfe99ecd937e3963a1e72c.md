

## 8.2

判断下列各题是*正确*还是*错误*。如果答案是*错误*，请解释原因。

- a) 地址运算符 `&` 只能用于常量和表达式。
- b) 声明为 `void *` 类型的指针可以被解引用。
- c) 一种类型的指针不能在不进行强制转换的情况下赋值给另一种类型的指针。

## 8.3

对于下列各项，编写执行指定任务的 C++ 语句。假设双精度浮点数存储在八个字节中，并且数组的起始地址位于内存位置 1002500。练习的每一部分应在适当情况下使用前面部分的结果。

- a) 声明一个名为 `numbers` 的 double 类型数组，包含 10 个元素，并将元素初始化为值 0.0、1.1、2.2、...、9.9。假设符号常量 `SIZE` 已定义为 10。
- b) 声明一个指向 double 类型变量的 `double` 指针 `nPtr`。
- c) 使用 `for` 语句，通过数组下标表示法打印数组 `numbers` 的元素。打印每个数字时保留小数点后一位精度。
- d) 编写两条单独的语句，每条都将数组 `numbers` 的起始地址赋给指针变量 `nPtr`。
- e) 使用 `for` 语句，通过指针 `nPtr` 的指针/偏移量表示法打印数组 `numbers` 的元素。
- f) 使用 `for` 语句，以数组名作为指针，通过指针/偏移量表示法打印数组 `numbers` 的元素。
- g) 使用 `for` 语句，通过指针 `nPtr` 的指针/下标表示法打印数组 `numbers` 的元素。
- h) 分别使用数组下标表示法、以数组名作为指针的指针/偏移量表示法、使用 `nPtr` 的指针下标表示法以及使用 `nPtr` 的指针/偏移量表示法引用数组 `numbers` 的第四个元素。
- i) 假设 `nPtr` 指向数组 `numbers` 的开头，`nPtr + 8` 引用的是什么地址？该位置存储的是什么值？
- j) 假设 `nPtr` 指向 `numbers[5]`，执行 `nPtr -= 4` 后，`nPtr` 引用的是什么地址？该位置存储的值是什么？

## 8.4

对于下列各项，编写一条执行指定任务的语句。假设浮点变量 `number1` 和 `number2` 已声明，并且 `number1` 已初始化为 7.3。假设变量 `ptr` 的类型为 `char *`。假设数组 `s1` 和 `s2` 都是 100 个元素的 char 数组，并且已用字符串字面量初始化。

- a) 声明变量 `fPtr` 为指向 double 类型对象的指针。
- b) 将变量 `number1` 的地址赋给指针变量 `fPtr`。
- c) 打印 `fPtr` 所指向对象的值。
- d) 将 `fPtr` 所指向对象的值赋给变量 `number2`。
- e) 打印 `number2` 的值。
- f) 打印 `number1` 的地址。
- g) 打印存储在 `fPtr` 中的地址。打印出的值与 `number1` 的地址相同吗？

## 8.5

执行下列各语句所指定的任务：

- a) 为名为 `exchange` 的函数编写函数头，该函数接受两个指向双精度浮点数的指针 `x` 和 `y` 作为参数，并且不返回值。
- b) 为 (a) 部分中的函数编写函数原型。
- c) 为名为 `evaluate` 的函数编写函数头，该函数返回整数，并接受整数 `x` 和指向函数 `poly` 的指针作为参数。函数 `poly` 接受一个整数参数并返回一个整数。
- d) 为 (c) 部分中的函数编写函数原型。
- e) 编写两条语句，每条都用元音字符串 "AEIOU" 初始化字符数组 `vowel`。

## 8.6

找出下列各程序段中的错误。假设有以下声明和语句：

```cpp
int *zPtr; // zPtr will reference array z
void *sPtr = 0;
int number;
int z[5] = { 1, 2, 3, 4, 5 };
```

- a) `++zPtr;`
- b)
  ```cpp
  // use pointer to get first value of array
  number = zPtr;
  ```
- c)
  ```cpp
  // assign array element 2 (the value 3) to number
  number = *zPtr[2];
  ```
- d)
  ```cpp
  // print entire array z
  for ( int i = 0; i <= 5; ++i )
      cout << zPtr[i] << endl;
  ```
- e)
  ```cpp
  // assign the value pointed to by sPtr to number
  number = *sPtr;
  ```
- f) `++z;`

## 自测练习答案

### 8.1

a) 地址。b) 0、NULL、一个地址。c) 0。

### 8.2

a) 错误。地址运算符的操作数必须是*左值*；地址运算符不能应用于常量或不会产生引用的表达式。

b) 错误。指向 void 的指针不能被解引用。这种指针没有类型，编译器无法确定要解引用的内存字节数以及指针所指向数据的类型。

c) 错误。任何类型的指针都可以赋给 void 指针。只有使用显式类型转换，void 类型的指针才能赋给其他类型的指针。

### 8.3

a)
```cpp
double numbers[ SIZE ] = { 0.0, 1.1, 2.2, 3.3, 4.4, 5.5, 6.6, 7.7, 8.8, 9.9 };
```

b)
```cpp
double *nPtr;
```

c)
```cpp
cout << fixed << showpoint << setprecision( 1 );
for ( int i = 0; i < SIZE; ++i )
    cout << numbers[ i ] << ' ';
```

d)
```cpp
nPtr = numbers;
nPtr = &numbers[ 0 ];
```

e)
```cpp
cout << fixed << showpoint << setprecision( 1 );
for ( int j = 0; j < SIZE; ++j )
    cout << *( nPtr + j ) << ' ';
```

f)
```cpp
cout << fixed << showpoint << setprecision( 1 );
for ( int k = 0; k < SIZE; ++k )
    cout << *( numbers + k ) << ' ';
```

g)
```cpp
cout << fixed << showpoint << setprecision( 1 );
for ( int m = 0; m < SIZE; ++m )
    cout << nPtr[ m ] << ' ';
```

h)
```cpp
numbers[ 3 ]
*( numbers + 3 )
nPtr[ 3 ]
*( nPtr + 3 )
```

i) 该地址是 1002500 + 8 * 8 = 1002564。值是 8.8。

j) `numbers[ 5 ]` 的地址是 1002500 + 5 * 8 = 1002540。  
`nPtr` 所引用的地址是 1002540 - 4 * 8 = 1002508。  
该位置的值是 1.1。

### 8.4

a) `double *fPtr;`

b) `fPtr = &number1;`

c) `cout << "The value of *fPtr is " << *fPtr << endl;`

d) `number2 = *fPtr;`

e) `cout << "The value of number2 is " << number2 << endl;`

f) `cout << "The address of number1 is " << &number1 << endl;`

g) `cout << "The address stored in fPtr is " << fPtr << endl;`

是的，该值相同。

### 8.5

a) `void exchange( double *x, double *y )`

b) `void exchange( double *, double * );`

c) `int evaluate( int x, int (*y)( int ) )`

d) `int evaluate( int, int (*)( int ) );`

e) `char vowel[] = "AEIOU";`

f) `char vowel[] = { 'A', 'E', 'I', 'O', 'U', '\0' };`

### 8.6

a) *错误：* zPtr 尚未初始化。  
*更正：* 用 `zPtr = z;` 初始化 zPtr。

b) *错误：* 指针未被解引用。  
*更正：* 将该语句改为 `number = *zPtr;`

c) *错误：* `zPtr[ 2 ]` 不是指针，不应被解引用。  
*更正：* 将 `*zPtr[ 2 ]` 改为 `zPtr[ 2 ]`。

d) *错误：* 使用指针下标引用数组边界之外的元素。  
*更正：* 为防止此问题，将 `for` 语句中的关系运算符改为 `<`，或将 `5` 改为 `4`。

e) *错误：* 解引用 void 指针。  
*更正：* 要解引用 void 指针，必须先将其转换为整数指针。将该语句改为 `number = *static_cast<int *>(sPtr);`

f) *错误：* 试图用指针算术修改数组名。  
*更正：* 使用指针变量代替数组名来完成指针算术，或对数组名使用下标以引用特定元素。

## 练习题

### 8.7 *（判断题）*

判断下列各题是*正确还是错误*。如果是错误，请解释原因。

- a) 指向不同数组的两个指针无法进行有意义的比较。
- b) 因为数组名是指向数组第一个元素的指针，所以数组名可以完全像指针一样被操作。

### 8.8 *（编写 C++ 语句）*

对于下列各项，编写执行指定任务的 C++ 语句。假设无符号整数存储在两个字节中，并且数组的起始地址位于内存位置 1002500。

- a) 声明一个名为 `values` 的 `unsigned int` 类型数组，包含五个元素，并将元素初始化为从 2 到 10 的偶数。假设符号常量 `SIZE` 已定义为 5。
- b) 声明一个指向 `unsigned int` 类型对象的指针 `vPtr`。
- c) 使用 `for` 语句，通过数组下标表示法打印数组 `values` 的元素。
- d) 编写两条单独的语句，每条都将数组 `values` 的起始地址赋给指针变量 `vPtr`。
- e) 使用 `for` 语句，通过指针/偏移量表示法打印数组 `values` 的元素。

