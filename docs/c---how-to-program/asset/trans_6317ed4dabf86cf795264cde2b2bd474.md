
```c
#include <stdio.h>
void f(const int *xPtr); // prototype

int main(void)
{
    int y; // define y

    f(&y); // f attempts illegal modification
}

// xPtr cannot be used to modify the
// value of the variable to which it points
void f(const int *xPtr)
{
    *xPtr = 100; // error: cannot modify a const object
}
```

`error C2166: l-value specifies const object`

**图 7.12** | 尝试通过指向常量数据的非常量指针修改数据。

正如你所知，数组是聚合数据类型，它在同一个名称下存储相关且类型相同的数据项。在第 10 章中，我们将讨论另一种聚合数据类型——结构（在其他语言中有时称为记录或元组）。结构能够在同一个名称下存储相关的数据项，这些数据项的类型可以相同也可以不同（例如，存储公司每个员工的信息）。当函数以数组作为参数被调用时，数组会自动按引用传递给函数。然而，结构总是按值传递——会传递整个结构的副本。这需要在执行时产生开销，即复制结构中的每个数据项并将其存储在计算机的函数调用栈上。当结构数据必须传递给函数时，我们可以使用指向常量的指针，以获得按引用传递的性能和按值传递的保护。当传递指向结构的指针时，只需要复制结构存储地址的副本。在地址为四字节的机器上，只复制四字节的内存，而不是可能很大的结构的副本。

> **性能提示 7.1**
> 使用指向常量的指针传递诸如结构之类的大对象，可以获得按引用传递的性能优势和按值传递的安全性。

如果内存有限且执行效率是关注点，请使用指针。如果内存充足且效率不是主要问题，则按值传递数据以强制执行最小权限原则。请记住，有些系统对 const 的强制执行不佳，因此按值传递仍然是防止数据被修改的最佳方式。

### 7.5.3 尝试修改指向非常量数据的常量指针

指向非常量数据的常量指针始终指向同一内存位置，并且可以通过该指针修改该位置的数据。这是数组名称的默认值。数组名称是指向数组开头的常量指针。数组中的所有数据都可以通过使用数组名称和数组索引来访问和更改。指向非常量数据的常量指针可用于接收数组作为函数参数，该函数仅使用数组索引表示法访问数组元素。声明为 const 的指针必须在定义时初始化（如果指针是函数参数，则它会用传递给函数的指针进行初始化）。图 7.13 尝试修改一个常量指针。指针 ptr 在第 12 行被定义为类型 `int * const`。该定义从 *right to left* 读作“ptr 是指向整数的常量指针”。指针在第 12 行用整数变量 x 的地址进行初始化。程序尝试将 y 的地址赋给 ptr（第 15 行），但编译器生成了错误信息。

```c
    1   // Fig. 7.13: fig07_13.c
    2   // Attempting to modify a constant pointer to non-constant data.
    3   #include <stdio.h>
    4
    5   int main(void)
    6   {
    7      int x; // define x
    8      int y; // define y
    9
    10     // ptr is a constant pointer to an integer that can be modified
    11     // through ptr, but ptr always points to the same memory location
    12     int * const ptr = &x;
    13
    14     *ptr = 7; // allowed: *ptr is not const
    15     ptr = &y; // error: ptr is const; cannot assign new address
    16  }
```

```text
c:\examples\ch07\fig07_13.c(15) : error C2166: l-value specifies const object
```

**图 7.13** | 尝试修改指向非常量数据的常量指针

### 7.5.4 尝试修改指向常量数据的常量指针

*最小访问权限* 由指向常量数据的常量指针授予。这样的指针始终指向 *相同* 的内存位置，并且该内存位置的数据 *不能被修改*。这就是应将数组传递给仅使用数组索引表示法查看数组且 *不* 修改数组的函数的方式。图 7.14 将指针变量 ptr（第 13 行）定义为类型 `const int *const`，从 *right to left* 读作“ptr 是指向整数常量的常量指针”。该图显示了当尝试 *modify* 的 *data* ptr 指向（第 16 行）以及当尝试 *modify* 指针变量中存储的 *address*（第 17 行）时生成的错误信息。

```c
    1   // Fig. 7.14: fig07_14.c
    2   // Attempting to modify a constant pointer to constant data.
    3   #include <stdio.h>
    4
    5   int main(void)
    6   {
    7       int x = 5; // initialize x
    8       int y; // define y
    9
    10      // ptr is a constant pointer to a constant integer. ptr always
    11      // points to the same location; the integer at that location
    12      // cannot be modified
    13      const int *const ptr = &x; // initialization is OK
    14
    15      printf("%d\n", *ptr);
    16      *ptr = 7; // error: *ptr is const; cannot assign new value
    17      ptr = &y; // error: ptr is const; cannot assign new address
    18  }
```

```text
c:\examples\ch07\fig07_14.c(16) : error C2166: l-value specifies const object
c:\examples\ch07\fig07_14.c(17) : error C2166: l-value specifies const object
```

**图 7.14** | 尝试修改指向常量数据的常量指针

## 7.6 冒泡排序[^3] 使用按引用传递

让我们改进图 6.15 中的冒泡排序程序，使用两个函数——bubbleSort 和 swap（图 7.15）。函数 bubbleSort 对数组进行排序。它调用函数 swap（第 46 行）来交换数组元素 array[j] 和 array[j + 1]。

```c
    1   // Fig. 7.15: fig07_15.c
    2   // Putting values into an array, sorting the values into
    3   // ascending order and printing the resulting array.
    4   #include <stdio.h>
    5   #define SIZE 10
    6
    7   void bubbleSort(int * const array, const size_t size); // prototype
    8
    9   int main(void)
   10  {
   11      // initialize array a
   12      int a[SIZE] = { 2, 6, 4, 8, 10, 12, 89, 68, 45, 37 };
   13
   14      puts("Data items in original order");
   15
   16      // loop through array a
   17      for (size_t i = 0; i < SIZE; ++i) {
   18          printf("%4d", a[i]);
   19      }
   20
   21      bubbleSort(a, SIZE); // sort the array
   22
   23      puts("\nData items in ascending order");
   24
   25      // loop through array a
   26      for (size_t i = 0; i < SIZE; ++i) {
   27          printf("%4d", a[i]);
   28      }
   29
   30      puts("");
   31  }
   32
   33  // sort an array of integers using bubble sort algorithm
   34  void bubbleSort(int * const array, const size_t size)
   35  {
   36      void swap(int *element1Ptr, int *element2Ptr); // prototype
   37
   38      // loop to control passes
   39      for (unsigned int pass = 0; pass < size - 1; ++pass) {
   40
   41          // loop to control comparisons during each pass
   42          for (size_t j = 0; j < size - 1; ++j) {
   43
   44              // swap adjacent elements if they're out of order
   45              if (array[j] > array[j + 1]) {
   46                  swap(&array[j], &array[j + 1]);
   47              }
   48          }
   49      }
   50  }
   51
   52  // swap values at memory locations to which element1Ptr and
   53  // element2Ptr point
   54  void swap(int *element1Ptr, int *element2Ptr)
   55  {
   56      int hold = *element1Ptr;
   57      *element1Ptr = *element2Ptr;
   58      *element2Ptr = hold;
   59  }
```

```text
Data items in original order
   2  6  4  8  10  12  89  68  45  37
Data items in ascending order
   2  4  6  8  10  12  37  45  68  89
```

**图 7.15** | 将值放入数组，按升序对值进行排序并打印结果数组

[^3]: 在第 12 章和附录 D 中，我们将研究性能更好的排序方案。
