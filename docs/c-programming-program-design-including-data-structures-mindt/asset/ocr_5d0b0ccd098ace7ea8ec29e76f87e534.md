The algorithm **max** is used to determine the maximum of two values. It has two forms, as given by the following prototypes:

```
template <class Type>
const Type& max(const Type& aVal, const Type& bVal);
```

```
template <class Type, class compare>
const Type& max(const Type& aVal, const Type& bVal, compare comp);
```

In the first form, the greater-than operator associated with **Type** is used. The second form uses the comparison operation specified by **comp**.

The algorithm **max_element** is used to determine the largest element in a given range. This algorithm has two forms, as given by the following prototypes:

```
template <class forwardItr>
forwardItr max_element(forwardItr first, forwardItr last);
```

```
template <class forwardItr, class compare>
forwardItr max_element(forwardItr first, forwardItr last,
                       compare comp);
```

The first form uses the greater-than operator associated with the data type of the elements in the range **first...last-1**. In the second form, the comparison operation specified by **comp** is used. Both forms return an iterator to the element containing the largest value in the range **first...last-1**.

The algorithm **min** is used to determine the minimum of two values. It has two forms, as given by the following prototypes:

```
template <class Type>
const Type& min(const Type& aVal, const Type& bVal);
```

```
template <class Type, class compare>
const Type& min(const Type& aVal, const Type& bVal, compare comp);
```

In the first form, the less-than operator associated with **Type** is used. In the second form, the comparison operation specified by **comp** is used.

The algorithm **min_element** is used to determine the smallest element in a given range. This algorithm has two forms, as given by the following prototypes:

```
template <class forwardItr>
forwardItr min_element(forwardItr first, forwardItr last);
```

```
template <class forwardItr, class compare>
forwardItr min_element(forwardItr first, forwardItr last,
                       compare comp);
```

The first form uses the less-than operator associated with the data type of the elements in the range **first...last-1**. The second form uses the comparison operation specified by **comp**. Both forms return an iterator to the element containing the smallest value in the range **first...last-1**.