```
```cpp
int main()
{
    int intList[] = {2, 56, 34, 25, 73,
                     46, 89, 10, 5, 16};                 //Line 1

    cout << "Line 2: Before sorting, intList: ";        //Line 2

    print(intList, 10);                                  //Line 3

    cout << endl;                                         //Line 4

    bubbleSort(intList, 10);                              //Line 5

    cout << "Line 6: After sorting, intList: ";         //Line 6

    print(intList, 10);                                   //Line 7

    return 0;
}

template <class elemType>
void print(elemType list[], int length)
{
    for (int i = 0; i < length; i++)
        cout << list[i] << " ";

    cout << endl;
}
```
```

# Sample Run:

```
Line 2: Before sorting, intList: 2 56 34 25 73 46 89 10 5 16

Line 6: After sorting, intList: 2 5 10 16 25 34 46 56 73 89
```

The statement in Line 1 declares and initializes intList to be an array of 10 components of type int. The statement in Line 3 outputs the values of the array intList before sorting this array. The statement in Line 5 uses the function bubbleSort to sort list. Notice that both intList and its length (the number of elements) are passed as parameters to the function bubbleSort. The statement in Line 7 outputs the sorted intList.

# Analysis: Bubble Sort

In the case of search algorithms, our only concern was with the number of key (item) comparisons. A sorting algorithm makes key comparisons and also moves the data. Therefore, in analyzing the sorting algorithm, we look at the number of key comparisons as well as the number of data movements.