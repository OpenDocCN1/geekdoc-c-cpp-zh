# Display 16.3  **Implementation of the Generic Sorting Function (part 2 of 2)**

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

# Tips  **How to Define Templates**

When we defined the function templates in Display 16.3, we started with a function that sorts an array of elements of type int. We then created a template by replacing the base type of the array with the type parameter T. This is a good general strategy for writing templates. If you want to write a function template, first write a version that is not a template at all but is just an ordinary function. Then completely debug the ordinary function, and finally convert the ordinary function to a template by replacing some types with a type parameter. There are two advantages to this method. First, when you are defining the ordinary function, you are dealing with a much more concrete case, which makes the problem easier to visualize. Second, you have fewer details to check at each stage; when worrying about the algorithm itself, you need not concern yourself with template syntax rules.

# Pitfall  **Using a Template with an Inappropriate Type**

You can use a template function with any type for which the code in the function definition makes sense. However, all the code in the template function must make sense and must behave in an appropriate way. For example, you cannot use the swapValues template (Display 16.1) with the type parameter replaced by a type for which the assignment operator does not work at all, or does not work “correctly.”