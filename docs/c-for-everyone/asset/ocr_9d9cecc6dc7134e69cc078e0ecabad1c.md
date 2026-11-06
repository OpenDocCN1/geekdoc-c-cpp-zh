# 6.2.8 Inserting an Element

If the order of the elements does not matter, you can simply insert new elements at the end, incrementing the variable tracking the size. (See Figure 8.) For a partially filled array:

Before inserting an element, move elements to the end of the array starting with the last one.

```
    if (current_size < CAPACITY)
    {
        current_size++;
        values[current_size - 1] = new_element;
    }
```

It is more work to insert an element at a particular position in the middle of a sequence. First, increase the variable holding the current size. Next, move all elements above the insertion location to a higher index. Finally, insert the new element. Here is the code for a partially filled array:

```
    if (current_size < CAPACITY)
    {
        current_size++;
        for (int i = current_size - 1; i > pos; i--)
        {
            values[i] = values[i - 1];
        }
        values[pos] = new_element;
    }
```

Note the order of the movement: When you remove an element, you first move the next element down to a lower index, then the one after that, until you finally get to the end of the array. When you insert an element, you start at the end of the array, move that element to a higher index, then move the one before that, and so on until you finally get to the insertion location (see Figure 9).

![](bbox=[0.15, 0.58, 0.45, 0.78])

![](bbox=[0.55, 0.58, 0.9, 0.78])

# 6.2.9 Swapping Elements

You often need to swap elements of an array. For example, the sorting algorithm in Special Topic 6.2 on page 263 sorts an array by repeatedly swapping elements.