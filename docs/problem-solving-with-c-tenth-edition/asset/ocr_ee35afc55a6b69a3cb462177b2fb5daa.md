# Helping functions

course, we also must adjust the helping functions so they apply to arrays of elements of type double. So let’s consider the helping functions that are called inside the body of the function sort. The two helping functions are swapValues and indexOfSmallest.

We already saw that swapValues can apply to variables of any type, provided we define it as a function template (as in Display 17.1). Let’s see if indexOfSmallest depends in any significant way on the base type of the array being sorted. The definition of indexOfSmallest is repeated next so you can study its details.

```
int indexOfSmallest(const int a[], int startIndex,
                    int numberUsed)
{
    int min = a[startIndex];
    int indexOfMin = startIndex;
    for (int index = startIndex + 1;
         index < numberUsed; index++)
    {
        if (a[index] < min)
        {
            min = a[index];
            indexOfMin = index;
            //min is the smallest of a[startIndex] through
            //a[index]
        }
    }
    return indexOfMin;
}
```

The function indexOfSmallest also does not depend in any significant way on the base type of the array. If we replaced the two highlighted instances of the type int with the type double, then we will have changed the function indexOfSmallest so that it applies to arrays whose base type is double.

To change the function sort so that it can be used to sort arrays with the base type double, we only needed to replace a few instances of the type name int with the type name double. Moreover, there is nothing special about the type double. We can do a similar replacement for many other types. The only thing we need to know about the type is that the operator < is defined for that type. This is the perfect situation for function templates. If we replace a few instances of the type name int (in the functions sort and indexOfSmallest) with a type parameter, then the function sort can sort an array of values of any type provided that the values of that type can be compared using the < operator. In Display 17.2 we have written just such a function template.

Notice that the function template sort shown in Display 17.2 can be used with arrays of values that are not numbers. In the demonstration program in Display 17.3, the function template sort is called to sort an array of characters. Characters can be compared using the < operator. Although the exact