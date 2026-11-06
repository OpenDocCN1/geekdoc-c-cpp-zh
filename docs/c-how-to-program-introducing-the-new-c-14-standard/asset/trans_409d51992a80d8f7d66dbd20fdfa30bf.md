
程序输出表明这些 `Arrays` 不相等。

### 用现有 `Array` 内容的副本初始化新的 `Array`

第37行实例化第三个 `Array`，名为 `integers3`，并用 `Array integers1` 的副本初始化它。这会调用类 `Array` 的复制构造函数，将 `integers1` 的元素复制到 `integers3` 中。我们稍后将讨论复制构造函数的细节。也可以通过如下方式编写第37行来调用复制构造函数：

```cpp
Array integers3 = integers1;
```

前面语句中的等号*不是*赋值运算符。当等号出现在对象的声明中时，它会调用该对象的构造函数。这种形式只能向构造函数传递一个参数——具体来说，就是 `=` 符号右侧的值。

第39–40行输出 `integers3` 的大小，然后输出 `integers3` 的内容，使用 `Array` 重载的流插入运算符来确认 `integers3` 的元素已由复制构造函数正确设置。

### 使用重载的赋值运算符

第44行通过将 `integers2` 赋值给 `integers1` 来测试重载的赋值运算符（`=`）。第46行显示两个 `Array` 对象的内容，以确认赋值成功。`Array` `integers1` 最初保存7个整数，但被调整大小以保存 `integers2` 中10个元素的副本。正如我们将看到的，重载的赋值运算符以对客户端代码透明的方式执行这种调整大小的操作。

### 使用重载的相等运算符

第51行使用重载的相等运算符（`==`）来确认在第44行赋值后，对象 `integers1` 和 `integers2` 确实*相同*。

### 使用重载的下标运算符

第56行使用重载的下标运算符来引用 `integers1[5]`——`integers1` 中的一个范围内的元素。这个带下标的名称被用作*右值*，以打印存储在 `integers1[5]` 中的值。第60行将 `integers1[5]` 用作赋值语句左侧的可修改*左值*，以将新值 `1000` 赋给 `integers1` 的第5个元素。我们将看到，在运算符确认 `5` 是 `integers1` 的有效下标后，`operator[]` 返回一个引用，用作可修改的*左值*。

第66行尝试将值 `1000` 赋给 `integers1[15]`——一个*越界*元素。在这个例子中，`operator[]` 确定下标越界，并抛出 `out_of_range` 异常。

有趣的是，数组下标运算符 `[]` 并不限于仅与数组一起使用；例如，它还可以用于从其他类型的*容器类*（如 `strings` 和字典）中选择元素。此外，当定义了重载的 `operator[]` 函数时，*下标不再必须是整数*——字符、字符串甚至用户定义类的对象也可以使用。在[第15章](#)中，我们讨论允许 `string` 下标的 Standard Library `map` 类。

## 10.10.2 `Array` 类定义

既然我们已经了解了这个程序如何运行，现在让我们逐步查看类头文件（图10.10）。当我们提到头文件中的每个成员函数时，我们会讨论图10.11中该函数的实现。在图10.10中，第32–33行表示类 `Array` 的 `private` 数据成员。每个 `Array` 对象由一个 `size` 成员（指示 `Array` 中元素的数量）和一个 `int` 指针——`ptr`——组成，该指针指向由 `Array` 对象管理的动态分配的基于指针的整数数组。

```cpp
// Fig. 10.10: Array.h
// Array class definition with overloaded operators.
#ifndef ARRAY_H
#define ARRAY_H

#include <iostream>

class Array {
   friend std::ostream& operator<<(std::ostream&, const Array&);
   friend std::istream& operator>>(std::istream&, Array&);

public:
   explicit Array(int = 10); // default constructor
   Array(const Array&); // copy constructor
   ~Array(); // destructor
   size_t getSize() const; // return size

   const Array& operator=(const Array&); // assignment operator
   bool operator==(const Array&) const; // equality operator

   // inequality operator; returns opposite of == operator
   bool operator!=(const Array& right) const {
      return !(*this == right); // invokes Array::operator==
   }

   // subscript operator for non-const objects returns modifiable lvalue
   int& operator[](int);

   // subscript operator for const objects returns rvalue
   int operator[](int) const;
private:
   size_t size; // pointer-based array size
   int* ptr; // pointer to first element of pointer-based array
};

#endif
```

图10.10 带重载运算符的 **Array** 类定义。

```cpp
// Fig. 10.11: Array.cpp
// Array class member- and friend-function definitions.
#include <iostream>
#include <iomanip>
#include <stdexcept>

#include "Array.h" // Array class definition
using namespace std;

// default constructor for class Array (default size 10)
Array::Array(int arraySize)
   : size{arraySize > 0 ? static_cast<size_t>(arraySize) :
          throw invalid_argument{"Array size must be greater than 0"}},
     ptr{new int[size]} { /* empty body */ }

// copy constructor for class Array:
// must receive a reference to an Array
Array::Array(const Array& arrayToCopy)
   : size{arrayToCopy.size}, ptr{new int[size]} {
      for (size_t i{0}; i < size; ++i) {
         ptr[i] = arrayToCopy.ptr[i]; // copy into object
      }
}

// destructor for class Array
Array::~Array() {
      delete[] ptr; // release pointer-based array space
}

// return number of elements of Array
size_t Array::getSize() const {
      return size; // number of elements in Array
}

// overloaded assignment operator:
// const return avoids: (a1 = a2) = a3
const Array& Array::operator=(const Array& right) {
   if (&right != this) { // avoid self-assignment
      // for Arrays of different sizes, deallocate original
      // left-side Array, then allocate new left-side Array
      if (size != right.size) {
          delete[] ptr; // release space
          size = right.size; // resize this object
          ptr = new int[size]; // create space for Array copy
      }

      for (size_t i{0}; i < size; ++i) {
          ptr[i] = right.ptr[i]; // copy array into object
      }
   }

   return *this; // enables x = y = z, for example
}

// determine if two Arrays are equal and
// return true, otherwise return false
bool Array::operator==(const Array& right) const {
   if (size != right.size) {
      return false; // arrays of different number of elements
   }

   for (size_t i{0}; i < size; ++i) {
      if (ptr[i] != right.ptr[i]) {
         return false; // Array contents are not equal
      }
   }

   return true; // Arrays are equal
}

// overloaded subscript operator for non-const Arrays;
// reference return creates a modifiable lvalue
int& Array::operator[](int subscript) {
   // check for subscript out-of-range error
   if (subscript < 0 || subscript >= size) {
      throw out_of_range{"Subscript out of range"};
   }

   return ptr[subscript]; // reference return
}

// overloaded subscript operator for const Arrays
// const return creates an rvalue
int Array::operator[](int subscript) const {
   // check for subscript out-of-range error
   if (subscript < 0 || subscript >= size) {
      throw out_of_range{"Subscript out of range"};
   }

   return ptr[subscript]; // returns copy of this element
}

// overloaded input operator for class Array;
// inputs values for entire Array
istream& operator>>(istream& input, Array& a) {
   for (size_t i{0}; i < a.size; ++i) {
      input >> a.ptr[i];
   }

   return input; // enables cin >> x >> y;
}

// overloaded output operator for class Array
ostream& operator<<(ostream& output, const Array& a) {
   // output private ptr-based array
   for (size_t i{0}; i < a.size; ++i) {
      output << a.ptr[i] << " ";
   }

   output << endl;
   return output; // enables cout << x << y;
}
```

图10.11 `Array` 类的成员函数和 `friend` 函数定义。
