
## FUNCTION TEMPLATE

The function definition and the function declaration for a function template are each prefaced with the following:

```
template<class Type_Parameter>
```

The function declaration (if used) and definition are then the same as any ordinary function declaration and definition, except that the Type_Parameter can be used in place of a type.

For example, the following is a function declaration for a function template:

```
template<class T>
void showStuff(int stuff1, T stuff2, T stuff3);
```

The definition for this function template might be as follows:

```
template<class T>
void showStuff(int stuff1, T stuff2, T stuff3)
{
    cout << stuff1 << endl
        << stuff2 << endl
        << stuff3 << endl;
}
```

The function template given in this example is equivalent to having one function declaration and one function definition for each possible type name. The type name is substituted for the type parameter (which is T in the example above). For instance, consider the following function call:

```
showStuff(2, 3.3, 4.4);
```

When this function call is executed, the compiler uses the function definition obtained by replacing T with the type name double. A separate definition will be produced for each different type for which you use the template, but not for any types you do not use. Only one definition is generated for a specific type regardless of the number of times you use the template.

## ALGORITHM ABSTRACTION

As we saw in our discussion of the swapValues function, there is a very general algorithm for interchanging the value of two variables that applies to variables of any type. Using a function template, we were able to express this more general algorithm in C++. This is a very simple example of algorithm abstraction. When we say we are using algorithm abstraction, we mean that we are expressing our algorithms in a very general way so that we can ignore incidental detail and concentrate on the substantive part of the algorithm. Function templates are one feature of C++ that supports algorithm abstraction.

## Example

## A GENERIC SORTING FUNCTION

Chapter 5 gave the selection sorting algorithm for sorting an array of values of type int. The algorithm was realized in C++ code as the function sort, given in Display 5.8. Below we repeat the definitions of this function sort:

```
void sort(int a[], int numberUsed)
{
    int indexOfNextSmallest;
    for (int index = 0; index < numberUsed - 1; index++)
    {//Place the correct value in a[index]:
        indexOfNextSmallest =
            indexOfSmallest(a, index, numberUsed);
        swapValues(a[index], a[indexOfNextSmallest]);
        //a[0] <= a[1] <=...<= a[index] are the smallest of the
        // original array elements. The rest of the elements
        //are in the remaining positions.
    }
}
```

If you study the above definition of the function sort you will see that the base type of the array is never used in any significant way. If we replaced the base type of the array in the function header with the type double, we would obtain a sorting function that applies to arrays of values of type double. Of course, we also must adjust the helping functions so that they apply to arrays of elements of type double. Let's consider the helping functions that are called inside the body of the function sort. The two helping functions are swapValues and indexOfSmallest.

We already saw that swapValues can apply to variables of any type for which the assignment operator works, provided we define it as a function template (as in Display 16.1). Let's see if indexOfSmallest depends in any significant way on the base type of the array being sorted. The definition of indexOfSmallest is repeated below so you can study its details.

```
int indexOfSmallest(const int a[], int startIndex, int numberUsed)
{
    int min = a[startIndex];
    int indexOfMin = startIndex;
    for (int index = startIndex + 1; index < numberUsed; index++)
        if (a[index] < min)
        {
            min = a[index];
            indexOfMin = index;
            //min is the smallest of a[startIndex] through a[index]
        }
    return indexOfMin;
}
```

The function indexOfSmallest also does not depend in any significant way on the base type of the array. If we replace the two highlighted instances of the type int with the type double, then we will have changed the function indexOfSmallest so that it applies to arrays whose base type is double.

To change the function sort so that it can be used to sort arrays with the base type double, we only need to replace a few instances of the type name int with the type name double. Moreover, there is nothing special about the type double. We can do a similar replacement for many other types. The only thing we need to know about the type is that the assignment operator and the operator, <, are defined for that type. This is the perfect situation for function templates. If we replace a few instances of the type name int (in the functions sort and indexOfSmallest) with a type parameter, then the function sort can sort an array of values of any type, provided that the values of that type can be assigned with the assignment operator and compared using the < operator. In Display 16.2 we have written just such a function template.

Notice that the function template sort shown in Display 16.2 can be used with arrays of values that are not numbers. In the demonstration program, the function template sort is called to sort an array of characters. Characters can be compared using the < operator, which compares characters according to the order of their ASCII numbers (see Appendix 3). Thus, when applied to two uppercase letters, the operator, <, tests to see if the first character comes before the second in alphabetic order. Also, when applied to two lowercase letters, the operator, <, tests to see if the first character comes before the second in alphabetic order. When you mix uppercase and lowercase letters, the situation is not so well behaved, but the program shown in Display 16.2 deals only with uppercase letters. In that program an array of uppercase letters is sorted into alphabetical order with a call to the function template sort. (The function template sort will even sort an array of objects of a class that you define, provided you overload the < operator to apply to objects of the class.)

Our generic sorting function has separated the implementation from the declaration of the sorting function by placing the definition of the sorting function in the file sort.cpp (Display 16.3). However, most compilers do not allow for separate compilation of templates in the usual sense. So, we have separated the implementation from the programmer’s point of view, but from the compiler’s point of view it looks like everything is in one file. The file sort.cpp is #included in our main file, so it is as if everything were in one file. Note that the #include directive for sort.cpp is placed before any invocation of the functions defined by templates. For most compilers this is the only way you can get templates to work.

## Display 16.2 A Generic Sorting Function (part 1 of 3)

```
//Demonstrates a template function that implements
//a generic version of the selection sort algorithm.
#include <iostream>
using std::cout;
using std::endl;

template<class T>
void sort(T a[], int numberUsed);
```

## Display 16.3 Implementation of the Generic Sorting Function (part 2 of 2)

```
```cpp
14  template<class T>
15  void swapValues(T& variable1, T& variable2)
      <the rest of the definition of swapValues is given in Display 16.1.>

16  template<class T>
17  int indexOfSmallest(const T a[], int startIndex, int numberUsed)
18  {
19      T min = a[startIndex];
20      int indexOfMin = startIndex;

21      for (int index = startIndex + 1; index < numberUsed; index++)
22      {
23          if (a[index] < min)
24          {
25              min = a[index];
26              indexOfMin = index;
27              //min is the smallest of a[startIndex] through a[index].
28          }
29      }

30      return indexOfMin;
31  }
```
```

## Tips How to Define Templates

When we defined the function templates in Display 16.3, we started with a function that sorts an array of elements of type int. We then created a template by replacing the base type of the array with the type parameter T. This is a good general strategy for writing templates. If you want to write a function template, first write a version that is not a template at all but is just an ordinary function. Then completely debug the ordinary function, and finally convert the ordinary function to a template by replacing some types with a type parameter. There are two advantages to this method. First, when you are defining the ordinary function, you are dealing with a much more concrete case, which makes the problem easier to visualize. Second, you have fewer details to check at each stage; when worrying about the algorithm itself, you need not concern yourself with template syntax rules.

## Pitfall Using a Template with an Inappropriate Type

You can use a template function with any type for which the code in the function definition makes sense. However, all the code in the template function must make sense and must behave in an appropriate way. For example, you cannot use the swapValues template (Display 16.1) with the type parameter replaced by a type for which the assignment operator does not work at all, or does not work “correctly.”
