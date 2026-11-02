```
if (values[i] > largest)
{
    largest = values[i];
}
}
for (int i = 0; i < current_size; i++)
{
    cout << values[i];
    if (values[i] == largest)
    {
        cout << " <= largest value";
    }
    cout << endl;
}
return 0;
}
```

# Program Run

```
Please enter values, Q to quit:
34.5 80 115 44.5 0
34.5
80
115 <= largest value
44.5
```

![](bbox=[0.1, 0.7, 0.2, 0.82])

# Special Topic 6.1

# Sorting with the C++ Library

You often want to sort the elements of an array or vector. Special Topic 6.2 shows you a sorting algorithm that is relatively simple but not very efficient. Efficient sorting algorithms are significantly more complex. Fortunately, the C++ library provides an efficient sort function.

To sort an array a with size elements, call

```
sort(a, a + size);
```

To sort a vector values, make this call:

```
sort(values.begin(), values.end());
```

![](bbox=[0.1, 0.88, 0.2, 0.99])

# Special Topic 6.2

# A Sorting Algorithm

A sorting algorithm rearranges the elements of a sequence so that they are stored in sorted order. Here is a simple sorting algorithm, called selection sort. Consider sorting the following array values:

[0] [1] [2] [3] [4]
11 9 17 5 12