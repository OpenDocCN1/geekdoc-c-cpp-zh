
```cpp
Volume(double a, double b, double c)
{
    len = a;
    wd = b;
    hgt = c;
    result = len * wd * hgt;
}
void CalcVol();
};
void Volume::CalcVol()
{
    cout << "Volume is: " << result << endl;
}
int main()
{
    Volume v1(5.2,3.4,7.3), v2(10,5,6);
    v1.CalcVol();
    v2.CalcVol();
    return 0;
}
```

### Output:

```text
Volume is: 129.064
Volume is: 300
```

In Listing 15, the Volume class includes an inline constructor. Volume(double a, double b, double c). Note that the use of the inline keyword is optional for an inline constructor, when the inline constructor is used within the class definition.

Listing 16 shows an example of an inline constructor outside a class by using the inline keyword (you can find this example in the InlineConstructor2.cpp file on the CD in the code\chapter6 folder):

## ▶ Listing 16: Creating an Inline Constructor outside a Class

```cpp
#include <iostream.h>

class Volume {
    double len, wd, hgt;
    double result;
public:
    Volume(double a, double b, double c);
    void CalcVol();
};
inline Volume::Volume(double a, double b, double c)
{
    len = a;
    wd = b;
    hgt = c;
    result = len * wd * hgt;
}

void Volume::CalcVol()
{
    cout << "Volume is: " << result << endl;
}

int main()
{
    Volume v1(5.2,3.4,7.3), v2(10,5,6);
    v1.CalcVol();
    v2.CalcVol();
    return 0;
}
```

### Output:

```text
Volume is: 129.064
Volume is: 300
```

In Listing 16, Volume(double a, double b, double c) is an inline constructor of the Volume class. The Volume(double a, double b, double c) constructor is defined outside the boundary of the Volume class by using the inline keyword and the scope resolution (::) operator.

## Copying a Constructor

As you know, it is possible to have a constructor with parameters. You can pass a constructor parameter as a value parameter of any data type, except an object of its own class. For example, in the following code snippet, the declaration of the Product class is invalid:

```cpp
class Product
{
...
...
public:
Product (Product object1);          // Invalid declaration
...
}
```

However, a class’s own object can be passed as a reference parameter. Reference parameters are indicated by an ampersand (&) symbol that precedes the argument. For example, in the following snippet, passing a reference argument of the Product class is valid:

```cpp
class Product
{
    ...
    ...
public:
    Product ();
    Product (Product &object1);        //copy constructor
    ...
};
```

A constructor having a reference to an object of its own class is known as a copy constructor. A copy constructor copies the data members from one object to another. Assume that o1 and o2 are the predefined objects of the Product class, as shown in the following code snippet:

```cpp
Product o1(200), o2(300);
o1=o2;
Product o3=o2;
```

In the preceding code snippet, the o1=o2; statement does not invoke the copy constructor even though both o1 and o2 are the objects of the same Product class. It is because the compiler copies the data from the o2 object to the o1 object, member by member, using the assignment (=) operator. The next statement, Product o3=o2, however, initializes one object with another object, during definition. The data members of the o2 object are copied to the o3 object, member by member. It is the default action performed by the copy of a constructor. The compiler executes the Product o3=o2 statement, as shown in the following code snippet:

```cpp
Product o3 (o2);
```

Listing 17 shows an example of creating a copy of the class constructor (you can find this example in the CopyConstructor.cpp file on the CD in the code\chapter6 folder):

### ▶ **Listing 17: Creating a Copy of a Constructor**

```cpp
#include <iostream.h>

class Product
{
    int number;
public:
    Product(int num);
    Product(Product &other_product);
    void displayNumber()
    {
        cout<<"The number is:"<<number<<endl;
    }
};
Product::Product(int num)
{
    number = num;
}
Product::Product(Product &other_product)
{
    number = other_product.number;
}

int main()
{
    Product o1(200),o2(300);
    o1=o2;
    Product o3=o2;
    cout<<"Value in Object1\n";
    o1.displayNumber();
    cout<<"Value in Object2\n";
    o2.displayNumber();
    cout<<"Value in Object3\n";
    o3.displayNumber();
    return 0;
}
```

### Output:

```text
Value in Object1
The number is:300
Value in Object2
The number is:300
Value in Object3
The number is:300
```

In Listing 17, the Product(Product &other_product) copy constructor takes only one argument, which is an object of the Product class and is passed by reference. In a copy constructor, it is essential to pass the reference of an object of a class. If the object of a class is passed as a value in the copy constructor, then multiple copies of the copy constructor are created. In addition, this process continues until or unless the system runs out of memory. Therefore, in a copy constructor, the argument must always be passed by reference to prevent creation of copies.

## TEST YOUR KNOWLEDGE

Q3. Create a program to display the use of copy constructor.

Ans.

```cpp
#include <iostream.h>
#include <string.h>
class StringClass {
    char *p;
public:
    StringClass(char *s);
    StringClass(StringClass &o);
    ~StringClass() {
        delete [] p;
    }
    char *get() {
        return p;
    }
};
StringClass::StringClass(char *s)
{
    int l;
    l = strlen(s)+1;
    p = new char [l];
    strcpy(p, s);
}
StringClass::StringClass(StringClass &o)
{
    int l;
    l = strlen(o.p)+1;
    p = new char [l];
    strcpy(p, o.p);
}
void show(StringClass x)
{
    char *s;
    s = x.get();
    cout << s << endl;
}
int main()
{
    StringClass a("www.kogent.com"), b("www.dreamtech.com");
    a=b;
    StringClass c=b;
    show(a);
    show(b);
    show(c);
    return 0;
}
```

### Output:

```text
www.dreamtech.com
www.dreamtech.com
www.dreamtech.com
```

## ■ Creating Dynamic Constructors

The constructors that can allocate the required amount of memory to objects at the time of their construction are known as dynamic constructors of objects. The memory is allocated with the help of the `new` operator. Listing 18 shows how to call dynamic constructors (you can find this example in the DynamicConstructor.cpp file on the CD in the `code\chapter6` folder):

### ▶ Listing 18: Calling Dynamic Constructors

```cpp
#include <iostream.h>

class AddingNumbers
{
  int *numPoint;
  int numSize;

public:
  AddingNumbers (int size)
  {
    numSize = size;
    numPoint = new int[size];
  }
  ~AddingNumbers ()
  {
    delete numPoint;
  }
  void input();
  void additionDisplay();
};

void AddingNumbers::input()
{
  for( int i = 0; i < numSize; i++ )
  {
    cout << "Enter a number at the position [ " << i << " ] ? ";
    cin >> numPoint [i];
  }
}
void AddingNumbers::additionDisplay()
{
  int sum=0;
  for( int i = 0; i < numSize; i++ )
    sum += numPoint [i];
  cout << "Sum of the numbers = " << sum;
}
void main()
{
  int num;
  cout << "How many numbers do you want to enter ?";
  cin >> num;
  // create an object of AddingNumber class and compute the sum of numbers
  AddingNumbers addnum (num);
  addnum.input();
  addnum.additionDisplay();
}
```

### Output:

```text
How many numbers do you want to enter ?5
Enter a number at the position [ 0 ] ? 10
Enter a number at the position [ 1 ] ? 20
Enter a number at the position [ 2 ] ? 30
Enter a number at the position [ 3 ] ? 40
Enter a number at the position [ 4 ] ? 50
Sum of the numbers = 150
```

In Listing 18, the following code snippet creates an instance (or an object) addnum of the AddingNumbers class dynamically by using the new operator:

```cpp
AddingNumbers addnum (num);
```

The object, addnum, is initialized with the num variable. The input() function accepts a number from a user, which indicates how many numbers are provided by a user. The additionDisplay() function adds all the number elements and displays their sum. When performing dynamic initialization of objects, it is important to note that the data members should not be initialized (pointer variable must be NULL). The parameterized constructor must allocate the right amount of memory resources. The program must have a destructor to release all the allocated memory.

## TEST YOUR KNOWLEDGE

- Q4. Create a program that can convert:
  - Meters into centimeters and vice-versa
  - Feet into inches and vice-versa

Ans:

```cpp
#include<iostream.h>

class db;
class dm
{
    private :
        float m,cm;
    public:
        dm():m(0.0),cm(0.0)
```
