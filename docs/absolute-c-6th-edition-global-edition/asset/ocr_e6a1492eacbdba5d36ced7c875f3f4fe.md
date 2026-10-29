# EXAMPLE: (continued)

base type of the array being sorted. The definition of indexOfSmallest is repeated next so you can study its details.

```
int indexOfSmallest(const int a[], int startIndex, int numberUsed)
{
    int min = a[startIndex],
    indexOfMin = startIndex;
    for (int index = startIndex + 1; index < numberUsed; index++)
        if (a[index] < min)
        {
            min = a[index];
            indexOfMin = index;
            //min is the smallest of a[startIndex] through
            //a[index]
        }
    return indexOfMin;
}
```

The function indexOfSmallest also does not depend in any significant way on the base type of the array. If we replace the two highlighted instances of the type int with the type double, then we will have changed the function indexOfSmallest so that it applies to arrays whose base type is double.

To change the function sort so that it can be used to sort arrays with the base type double, we need only to replace a few instances of the type name int with the type name double. Moreover, there is nothing special about the type double. We can do a similar replacement for many other types. The only thing we need to know about the type is that the assignment operator and the operator <, are defined for that type. This is the perfect situation for function templates. If we replace a few instances of the type name int (in the functions sort and indexOfSmallest) with a type parameter, then the function sort can sort an array of values of any type, provided that the values of that type can be assigned with the assignment operator and compared using the < operator. In Display 16.2, we have written just such a function template.

Notice that the function template sort shown in Display 16.2 can be used with arrays of values that are not numbers. In the demonstration program, the function template sort is called to sort an array of characters. Characters can be compared using the < operator, which compares characters according to the order of their ASCII numbers (see Appendix 3). Thus, when applied to two uppercase letters, the operator <, tests to see if the first character comes before the second in alphabetical order. Also, when applied to two lowercase letters, the operator <, tests to see if the first character comes before the second in alphabetical order. When you mix upper- and lowercase letters, the situation is not so well behaved, but the program shown in Display 16.2 deals only with uppercase letters. In that program, an array of uppercase letters is sorted into alphabetical order with a call to the function template sort. (The function template sort will even sort an array of objects of a class that you define, provided you overload the < operator to apply to objects of the class.)