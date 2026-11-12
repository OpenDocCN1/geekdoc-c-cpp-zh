
```cpp
int b=1;
cout<<a<<"\n"<<b<<"\n"<<c;
}
int main()
{
func ();
func (10);
func (10,20.000);
return 0;
}
```

- (a) Compilation error
- (b) 1,1,a
- (c) Syntax error
- (d) 10,20,000

**Answer:** (a) Compilation error. Declaration of `int a` and `int b` shadows the default values and is not permitted.

## 25. What is the output of the following code? (L4)

```cpp
#include <iostream>
using namespace std;
void func (int a=0, int b=0, char c = 'a')
{
cout <<"\n" << a;
cout <<"\n" << b;
cout << "\n" << c;
}
int main()
{
func ();
func (10);
func (10,20.000);
return 0;
}
```

- (a) Compilation fault
- (b) Overloading error
- (c)
  ```text
  0
  0
  a
  10
  0
  a
  10
  20
  a
  ```
- (d) None of the above

**Answer:** (c) The code will get compiled normally and one more variable in the function definition will not change the course of flow.

## 26. What is the output of the following code? (L4)

```cpp
#include <iostream>
using namespace std;
void func (int a=0,int a=1, int b=0, char c = 'a')
{
cout <<"\n" << a;
cout <<"\n" << b;
cout << "\n" << c;
}
int main() {
func ();
func (10);
func (10,20.000);
return 0;
}
```

- (a) Compilation error
- (b)
  ```text
  1
  0
  a
  10
  0
  a
  ```
- (c)
  ```text
  0
  0
  a
  10
  0
  a
  ```

```cpp
int x=9, y=7;
ambiguity_learn (x,y);
return 0;
}
```

- (a) 16
- (b) 63
- (c) Compilation error
- (d) None of the above

**Answer:** (c) Call of the overloaded `ambiguity_learn(int&, int&)` is ambiguous. There is no difference from syntax point of view for calling a function with a value and with a reference.

## 30. What is the output of the following code? (L4)

```cpp
#include <iostream>
using namespace std;
void func (int a, int b=1)
{
cout<<a<<",";
cout<<b<<" ";
}
void func (int a)
{
cout<<a<<" ";
}
int main() {
func (10);
func (10,20);
return 0;
}
```

- (a) 10 10 20
- (b) 10 20 10
- (c) Compilation error
- (d) Syntax error

**Answer:** (c) It is ambiguous here as func(10) call matches both the functions hence, it is ambiguous.

## 31. What is the OOPS feature used in the following code? (L1)

```cpp
#include <iostream>
using namespace std;
class base_class {
public:
void function_foo ()
{
cout <<"Hello, I am in base class" << endl;
}
};
class derived_class : public base_class {
public:
void function_foo ()
{
cout <<"Hello, I am in derived class" << endl;
}
};
int main ()
{
base_class b;
b.function_foo();
derived_class d;
d.function_foo();
getchar ();
return 0;
}
```

- (a) Operator overloading
- (b) Function overloading
- (c) Function overriding
- (d) None of the above

**Answer:** (c) It is function overriding. The function `function_foo` has different contents in the base class and derived class thus, overriding the function.

## 32. What would be the output of the following code? (L1)

```cpp
#include <iostream>
using namespace std;

class base_class {
public:
    void function_foo ()
    {
        cout <<"Hello, I am in base class" << ", ";
    }
};
class derived_class : public base_class {
public:
    void function_foo ()
    {
        cout <<"Hello, I am in derived class" << ", ";
    }
};
int main ()
{
    base_class b;
    b.function_foo();
    derived_class d;
    d.function_foo();
    getchar ();
    return 0;
}
```

- (a) Hello, I am in base class,Hello, I am in base class
- (b) Hello, I am in base class,Hello, I am in derived class
- (c) Hello, I am in derived class,Hello, I am in derived class
- (d) Syntax error

**Answer:** (b) Since the function is overridden successfully, it will call the functions appropriately for each function call. Base class object will call base class function and derived class object will call derived class function.

## 33. What would be the output of the following code? (L1)

```cpp
#include <iostream>
using namespace std;
class base_class {
public:
    void function_foo ()
    {
        cout <<"Hello, I am in base class" << ", ";
    }
};
class derived_class : private base_class {
public:
    void function_foo ()
    {
        cout <<"Hello, I am in derived class" << ", ";
    }
};
int main ()
{
    base_class b;
    b.function_foo();
    derived_class d;
    d.function_foo();
    return 0;
}
```

- (a) Hello, I am in base class,Hello, I am in base class
- (b) Hello, I am in base class,Hello, I am in derived class
- (c) Hello, I am in derived class,Hello, I am in derived class
- (d) Syntax error

**Answer:** (b) Deriving the class with private rights has not affected the overridden function. Since the function is overridden successfully, it will call the functions appropriately for each function call. Base class object will call base class function and derived class object will call derived class function.

## 34. Which of the following points hold good for function overriding? (L2)

1. The definition of the function being overridden must have same method name.
2. The base class function and the overriding function must have same data type.
3. The base class function and the overriding function must have same argument list.
4. The derived class must be inherited only with private access rights.

- (a) 1, 2
- (b) 1, 2, 3
- (c) 1, 2, 3, 4
- (d) 4

**Answer:** (b) 1,2 and 3 are true with respect to function overriding. It is referred to as signature.

## 35. What is the output of the following code? (L2)

```cpp
#include <iostream>
using namespace std;
class base_class {
public:
    int c;
    void function_foo (int a, int b)
    {
        c = a + b;
        cout <<endl << c;
    }
};
class derived_class : private base_class {
public:
    int d;
    void function_foo (int e, int f)
    {
        d = e + f;
        cout<<d<<" ";
    }
};
int main ()
{
    base_class b;
    b.function_foo(3, 4);
    derived_class d;
    d.function_foo(4, 5);
    return 0;
}
```

- (a) 3 5
- (b) 7 9
- (c) 9 7
- (d) Error

**Answer:** (b) Since the data type, number of arguments everything goes as per the rule referred in Question number 34, the code will work fine and overriding will happen. The output of the code would be 7, 9.

## 36. Identify mistakes if any in the following code. (L2)

```cpp
#include <iostream>
using namespace std;
class base_class {
public:
    float c;
    void function_foo (float a, float b)
    {
        c = a + b;
        cout <<endl << c;
    }
};
class derived_class : private base_class {
public:
    int d;
    void function_foo (int e, int f)
    {
        d = e + f;
        cout << endl << d;
    }
};
int main ()
{
    base_class b;
    b.function_foo(3.222, 4.568);
    derived_class d;
    d.function_foo(4, 5);
    return 0;
}
```

1. The definition of the function being overridden must have same method name.
2. The base class function and the overriding function must have same data type.
3. The base class function and the overriding function must have same argument list.
4. Everything is fine and no rule is broken.

- (a) 1 and 2
- (b) 1, 2 and 3
- (c) 2
- (d) 4

**Answer:** (c) The base class function and the overriding function must have same data type and this rule is not followed in the above code snippet.

## 40. Which of the following types of inheritances supports overriding? (L3)

1. Multiple inheritance
2. Multilevel inheritance
3. Single inheritance
4. Hybrid inheritance
5. All the above

- (a) 1, 2, 3
- (b) 1, 3
- (c) 5
- (d) 1

**Answer:** (c) All the types of inheritances support overriding.

## 41. Which of the following is true about virtual functions? (L1)

- (a) Virtual functions will enable the programmer to redefine the functions declared in the base class in derived class.
- (b) No specific keywords are required to make a function virtual.
- (c) Virtual function enables early binding or compile time binding.
- (d) Virtual function enables late binding or runtime binding.

**Answer:** (a) and (d) are true.

## 42. Which of the following is said to be late binding? (L2)

- (a) A function call is resolved at runtime.
- (b) Compiler will determine object type at runtime, and will bind the function call.
- (c) Compiler determines the object type well in advance and binds it in time.
- (d) None of the above.

**Answer:** (a) and (b)

## 43. True or False

Virtual functions also follow the same principle of one interface and multiple methods like polymorphism. (L1)

**Answer:** True. It is referred as runtime polymorphism.

## 44. True or False

A class if using virtual function can be referred by the term polymorphic class. (L1)

**Answer:** True.

## 45. Which of the following are wrong about virtual functions? (L1)

- (a) It is one of the member functions of a class and carries no additional privilege.
- (b) The keyword `virtual` is used to make a function virtual function.
- (c) Provides no different functionality in the derived class.
- (d) `virtual` keyword has to be used only in upper case letters.
