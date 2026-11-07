The following statement derives the `class stockListType` from the `class listType`.

```
```cpp
class stockListType: public listType<stockType>
{
    member list
};
```
```

The member variables to hold the list elements, the length of the list, and the max listSize were declared as `protected` in the `class listType`. Therefore, these members can be directly accessed in the `class stockListType`.

Because the company also requires you to produce the list ordered by the percent gain/loss, you need to sort the stock list by this component. However, you are not to physically sort the list by the component percent gain/loss. Instead, you will provide a logical ordering with respect to this component.

To do so, add a member variable, an array, to hold the indices of the stock list ordered by the component percent gain/loss. Call this array `sortIndicesGainLoss`. When printing the list ordered by the component percent gain/loss, use the array `sortIndicesGainLoss` to print the list. The elements of the array `sortIndicesGainLoss` will tell which component of the stock list to print next.

+   c. Write a program that uses these two classes to automate the company’s analysis of stock data.

+   19. Write the definitions of the member functions of the `classes` `arrayListType` and `unorderedArrayListType` that are not given in this chapter. Also, write a program to test your function.

+   20. Write the definition of the `class template` `orderedArrayListType`, derived from the `class arrayListType`, to implement an ordered list. As in Chapter 12, add the function insert to this class. Provide the definitions of the nonabstract functions. Also, write a program to test your class.

+   21. **(Unordered Sets)** Redo Programming Exercise 12 of Chapter 12 using templates.

+   22. **(Ordered Sets)** Redo Programming Exercise 13 of Chapter 12 using templates.