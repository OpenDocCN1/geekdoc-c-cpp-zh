
The operator function in the program uses the library function strcmp to compare two C strings. The library function strcmp returns a zero in case of exact match; otherwise, it returns an integer value depending on the input strings supplied to it as input parameters.

Now, after discussing operator overloading, a question might arise whether all the operators in C++ can be overloaded or not. Let's find the answer to this question in the next section.

## Operator Overloading Restrictions

There are some restrictions that apply to operator overloading. We cannot alter the precedence of an operator. In addition, we cannot change the number of operands that an operator takes; however, we can ignore one operand by using default argument. Moreover, operator functions cannot have default arguments. Finally, we cannot overload all the operators in C++. The set of operators that cannot be overloaded are as follows:

- `.`, `::`, `?:`, `.*`

Now that we are free to perform any activity within an operator function. For example, we can overload the ‘+’ operator for a class and write “Inside Overloaded Operator +” ten times to a disk file. However, this is not advisable because the chances of mishandling operator overloading in a large program can increase as we deviate from the original meaning of the operator function. For example, while overloading the ‘+’ operator, instead of performing addition, we can write a string to a disk file. However, at the time of software maintenance, when some other programmer examines the code, he/she can assume that the ‘+’ operator is used to add two objects. Therefore, it is not advisable to decouple the original meaning of the operator from it.

Note: Except for the ‘=’ operator, operator functions are inherited by any derived class. However, a derived class is free to overload any operator, irrespective of the fact that the base class has also overloaded it or not. In this case, the derived class object will use its own operator function, as it will override the operator function of the base class. We learn more about inheritance later in the chapter.

In the next section, let’s learn how to overload some special operators in C++.

## Overloading Some Special Operators

Till now, we have overloaded some common operators, such as ‘==’, ‘+’, ‘-’, and ‘++’, but there are some special operators that can be overloaded as well. These special operators are the array subscript operator ‘[]’, the parenthesis operator ‘()’, and the dereferencing operator ‘->’. The most important thing to note about these three operators is that they must be non-static member functions and they cannot be friends.

In C++, the array subscript operator is overloaded as a binary operator. Consider the following example for an integer array:

```cpp
int className::operator[](int i)
{
    // Definition
}
```

Technically, the parameter does not really have to be of type int, but as we are overloading the array subscript operator, generally an integer value is used. Suppose the following expression is used:

```cpp
Arrayobj[5];
```

Then, the preceding expression would translate into the call to the operator[] function as follows:

```cpp
operator[](5);
```

Listing 14.3 shows how to overload the array subscript operator.

Listing 14.3: Showing the Working of Overloaded Array Subscript Operator

```cpp
1:/* Operator Overloading Example Program 8 */
2:#include <iostream>
3:using namespace std;
4:
5:class Example {
6:    int array[2];
7:public:
8:Example()
9:{
10:    array[0] = array[1] = 0;
11:}
12:Example(int val1, int val2)
13:{
14:    array[0] = val1;
15:    array[1] = val2;
16:}
17:int operator[](int i)
18:{
19:    return array[i];
20:}
21:};
22:
23:int main()
24:{
25:    Example obj(3,6);
26:
27:        cout<<obj[1]<<endl;
28:
29:        return 0;
30:}
```

In the preceding program, the Example class defines an array of two integers, which is initialized by using a constructor function in line number 12. The constructor function initializes each member of the array to a specific value. The overloaded operator [] function returns the value of the array as indexed by the value of its parameters. This way, we can only use the array subscript on the right side. However, we can design the operator [] function in such a way that it can be used on both the left and right sides of the assignment statement. To do this, we need to specify the return value of the [] operator function as a reference, as shown in the following code snippet:

```cpp
int &operator[](int i)
{
    return array[i];
}
```

By replacing the operator function in Listing 14.3 with the preceding code snippet, we can use the array subscript operator on both sides of the assignment operator.

Let's now handle a real-life scenario using the overloaded array subscript operator. At times, while programming, we commit mistakes by accessing elements from an array with out-of-bound index. The following program uses the overloaded array subscript operator to check the out-of-bound index while inserting values into an array:

```cpp
1:/* Operator Overloading Example Program 9 */
2:#include <iostream.h>
3:#include <stdlib.h>
4:using namespace std;
5:
6:class SafeArray {
7:    int array[4];
8:public:
9:SafeArray()
10:    {
11:        array[0] = array[1] = array[2] = array[3] = 0;
12:    }
13:    SafeArray(int val1, int val2, int val3, int val4)
14:    {
15:        array[0] = val1;
16:        array[1] = val2;
17:        array[2] = val3;
18:        array[3] = val4;
19:    }
20: int &operator[](int i)
21: {
22:     if (i<0 || i>3) {
23:         cout<<"Boundary Error"<<endl;
24:         exit(1);
25:     }
26:     return array[i];
27: }
28:};
29:
30:int main()
31:{
32:    SafeArray obj(3, 6, 9, 15);
33:
34:    cout<<obj[1]<<endl;
35:
36:    obj[1] = 190;
37:    cout<<obj[1]<<endl;
38:
39:    obj[4] = 59;  // Runtime Error - Out of Bound Index
40:
41:    return 0;
42:}
```

In line number 34, we have accessed the data element at array index 1. The compiler does not raise any error while executing this line and provides the requested data element. Now in line number 36, we have again accessed the array element at index 1 to assign a new data member into this location. As we use the reference in the operator [] function definition, the compiler proceeds with it successfully. Now, the main purpose of writing this program can be figured out when we try to execute line number 39. For invalid and out-of-bound access of array index, as soon as this statement is executed using the array subscript operator, the compiler raises the error message, Boundary Error. In addition, if the operator has not been overloaded, then the program terminates with runtime error.

Now, let's overload the parenthesis operator. Usually we write a separate member routine, which sets the value of the object at any point in a program. However, at times, in the middle of a program, we want to change the value of an object or reinitialize it without using the constructor function. Therefore, it would be nice if we could do this, as easily as the constructor does this at the time of definition. To solve this problem, we can overload the parenthesis operator. The overloaded parenthesis operator will behave similarly to the constructor function block and can be called at any point of the program execution. Let's implement this functionality in the following program:

```cpp
1:/* Operator Overloading Example Program 10 */
2:#include <iostream.h>
3:using namespace std;
4:
5:class Example {
6:      int var1;
7:      int var2;
8:public:
9:Example()
10:    {
11:        var1 = var2 = 0;
12:    }
13:    Example(int val1, int val2)
14:    {
15:        var1 = val1;
16:        var2 = val2;
17:    }
18:    void show()
19:    {
20:        cout<<"Var1 = "<<var1<<" Var2 = "<<var2<<endl;
21:    }
22:    Example operator()(int i, int j)
23:    {
24:        var1 = i;
25:        var2 = j;
26:        return *this;
27:    }
28:};
29:
30:int main()
31:{
32:    Example obj1(3, 6);
33:    Example obj2;
34:
35:    obj1.show();
36:    obj2.show();
37:
38:    obj2(5,7);
39:
40:    obj1.show();
41:    obj2.show();
42:
43:    return 0;
44:}
```

In the preceding program, line number 38 uses the similar syntax as line number 32 and operates in a similar way from the user's perspective. Following is the output of the preceding program:

```
Var1 = 3 Var2 = 6
Var1 = 0 Var2 = 0
Var1 = 3 Var2 = 6
Var1 = 5 Var2 = 7
```

Let's now learn how to overload the dereferencing operator (->). The dereferencing operator is considered as a unary operator while overloading. The following is the syntax of using the dereferencing operator:

```cpp
Object->element;
```

In the preceding syntax, object activates the call to the operator ->() function, which must return a pointer to an object of the class that operator ->() function operates on. The element must be one of the member variables of a class. The following program shows how to overload the dereferencing operator in C++:

```cpp
1:/* Operator Overloading Example Program 10 */
2:#include <iostream.h>
3:using namespace std;
```
