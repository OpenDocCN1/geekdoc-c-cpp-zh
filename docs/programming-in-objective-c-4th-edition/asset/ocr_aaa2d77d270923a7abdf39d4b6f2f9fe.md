```
result = [*fractsPtr add: *(fractsPtr + 1)];
```

The increment and decrement operators (++ and --) are particularly handy when dealing with pointers. Applying the increment operator to a pointer has the same effect as adding 1 to the pointer, whereas applying the decrement operator has the same effect as subtracting 1 from the pointer (here "1" means one unit, or the size of the data item the pointer is declared to point to). So if textPtr were defined as a char pointer and were set to point to the beginning of an array of chars text, the statement

```
++textPtr;
```

would textPtr to point to the next character in text, which is text[1]. In a similar fashion, the statement

```
--textPtr;
```

would textPtr to point to the previous character in text (assuming, of course, textPtr was not pointing to the beginning of text before this statement executed.

Comparing two pointer variables in Objective-C is perfectly valid. This is particularly useful when comparing two pointers in the same array. For example, you could test the pointer valuesPtr to see whether it points past the end of an array containing 100 elements by comparing it to a pointer to the last element in the array. So the expression

```
valuesPtr > &values[99]
```

would be TRUE (nonzero) if valuesPtr was pointing past the last element in the values array, and it would be FALSE (zero) otherwise. From our earlier discussions, you can replace the previous expression with its equivalent: