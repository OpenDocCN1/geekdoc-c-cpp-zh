
passed to it, however the function will not produce correct results if any other type of values are passed to it.

For instance, if we call the function add() by passing float values

```cpp
float k = add(10.2, 11.5);
```

the value returned in variable k will not be correct; rather, it will be truncated. As per the default behaviour of C++, value in variable k will be 21.00 and not 21.7. This means that the function has performed truncation of the resultant value resulting in loss of data. And hence, the function cannot work for float type values.

At times, it is required to implement the same logic for multiple types of values. In such cases, you can use function templates in C++. Function templates enable the programmer to create a function, which can give correct results for different types of data values. The following is the syntax of creating function template:

```cpp
template<class G1, class G2, class G3, ..., class Gn>
```

Function Definition of generic function which uses generic types

```text
G1, G2, G3, ..., Gn
```

Note that the first line in the syntax informs the compiler that G1, G2, G3, ..., Gn are generic data types which can take different forms when the function call is made. The second line in the syntax then actually defines the generic function.

For example, consider the function definition of generic add() function as shown below:

```cpp
template<class G>
G add(G a, G b)
{
    G c = a + b;
    return c;
}
```

The statement

```cpp
template<class G>
```

informs the compiler that G is a generic type on which the defined function will operate. Whereas the function add() has a return type as G, and both its arguments a and b are also of type G. The type G will take the correct data type depending on the data type of values passed to function add() when the function is called. The following is the full source code which shows the creation of template function add():

```cpp
#include<iostream.h>
template<class G>
G add(G a, G b)
{
    G c = a + b;
    return c;
}

void main()
{
    int x, y, res1;
    float p, q, res2;
    cout << "Enter values of x and y" << endl;
    cin >> x >> y;
    res1 = add(x, y);
    cout << "Addition of x and y is " << res1 << endl;

    cout << "Enter values of p and q" << endl;
    cin >> p >> q;
    res2 = add(p, q);
    cout << "Addition of p and q is " << res2 << endl;
}
```

**Output**

```text
Enter values of x and y
10 20
Addition of x and y is 30
Enter values of p and q
10.3 20.6
Addition of p and q is 30.9
```

In the first function call

```cpp
res1 = add(x, y);
```

type G takes a form of int. This is because the data type of x, y and res1 is int. This means that the function add() performs addition of integers in response to this call. The second function call

```cpp
res2 = add(p, q);
```

makes G take the form of float because variables p, q and res2 are of type float. Hence, the function call results in correctly calculating addition of two floating point numbers, thereby printing the result without any truncation as seen in the output of the program.

**CAUTION**

Refer main() function below.

```cpp
void main()
{
    int x;
    float y, res1;
    cout << "Enter values of x and y" << endl;
    cin >> x >> y;
    res1 = add(x, y); // ERROR - Incorrect function call
    cout << "Addition of x and y is " << res1 << endl;
}
```

The call made to `add()` within `main()` will not work and will raise an error. This is because we have created only one generic type G, and it can take only one form at a time. The function call passes x and y as arguments in which x is of type integer and y is of type float. If you see the function definition of `add()`, both the arguments must be of a single type G. However, in this case, we have erroneously passed arguments of different types to `add()` which results in a compilation error. The exact error message is as shown below:

```text
[Error]: No matching function for call to 'add (int&, float&)'
```

**NOTES**

It is possible to create multiple generic types while defining a function. For example, in the code below we have created two generic types G1 and G2, and they can take different forms for a single function call.

```cpp
#include<iostream.h>
template<class G1, class G2>
G2 add(G1 a, G2 b)
{
    G2 c = a + b;
    return c;
}

void main()
{
    int x;
    float y, res1;
    cout << "Enter values of x and y" << endl;
    cin >> x >> y;
    res1 = add(x, y);
    cout << "Addition of x and y is " << res1 << endl;
}
```

**Output**

```text
Enter values of x and y
10 20.5
Addition of x and y is 30.5
```

The function call

```cpp
res1 = add(x, y);
```

forces G1 to take the form of int (because x is of type int) and G2 to take the form of float (because y is of type float). Note that the function returns G2 because variable c inside add() is created of type G2. This makes sense because addition of int and float is always a float, and G2 is the generic type which has taken a form of float for this function call.

Had it been that the function call to add() was

```cpp
res1 = add(y, x);
```

it would not have resulted in a correct result because first argument y forces G1 to take the form of float, and second argument x forces G2 to take the form of int. In the function body, we return c which is the result of addition. The problem is that the data type of result is G2 which is of type int. Hence, this will result in truncation of the resultant value. Clearly, this is a logical error because the function call is not made correctly by the programmer. It is the programmer's responsibility to use template functions correctly to avoid such logical errors.

### 16.3 Class Templates

Class templates are used to define generic classes. A generic class is a class which can have generic members and generic member functions. The actual data types which the generic types convert into must be specified while creating an instance of the class.

```cpp
template<class G1, class G2, class G3, ..., class Gn>
```

Class definition using generic types G1, G2, G3, ..., Gn

Note that the first line in the syntax informs the compiler that G1, G2, G3, ..., Gn are generic data types, which can take different forms each time a class is instantiated. The second line in the syntax actually defines the generic class. Given below is an example which creates a class Data using two generic types G1 and G2:

```cpp
#include<iostream.h>
template<class G1, class G2>
class Data
{
private:
    G1 a;
    G2 b;
public:
    void input()
    {
        cout << "Enter values of a and b" << endl;
        cin >> a >> b;
    }
    void add()
    {
        cout << "Addition of a and b is " << a + b << endl;
    }
};

void main()
{
    // Addition of two integers
    Data<int, int> o1;
    o1.input();
    o1.add();

    // Addition of one integer and one float
    Data<int, float> o2;
    o2.input();
    o2.add();

    // Addition of two floats
    Data<float, float> o3;
    o3.input();
    o3.add();
}
```

**Output**

```text
Enter values of a and b
10 20
Addition of a and b is 30
Enter values of a and b
10 30.5
Addition of a and b is 40.5
Enter values of a and b
44.5 44.3
Addition of a and b is 88.8
```

The statement

```cpp
template<class G1, class G2>
```

is present just before defining class `Data`. This statement informs the compiler that `G1` and `G2` are two generic types which will be used while defining class `Data`. In fact, if you see the definition of class `Data`, it contains members `a` and `b` of type `G1` and `G2`, respectively. The member function `input()` takes the members `a` and `b` as input from the user, whereas the function `add()` performs the addition and prints the result on computer screen.

The first statement of `main()`

```cpp
Data<int, int> o1;
```

creates an object `o1` of class `Data`. Note that we have specified actual data types in triangular brackets for `G1` and `G2`. The generic tag `<int,int>` informs the compiler that the generic types `G1` and `G2` should take the form of `int`, for object `o1`.

Whereas the statement

```cpp
Data<int, float> o2;
```

creates another object of class `Data` named as `o2`. This time, we have specified the tag as `<int,float>` which means that the first generic type `G1` will take a form of `int` and second generic type `G2` will take a form of `float` for this instance. Therefore, the member `a` of object `o2` is an `int` and member `b` of object `o2` is a `float`. Whereas both the members of object `o1` are integers as shown in Figure 16.1.

**NOTES**

Objects of same class `o1` and `o2` have different sizes because the data type of their members is different as shown in Figure 16.1.
