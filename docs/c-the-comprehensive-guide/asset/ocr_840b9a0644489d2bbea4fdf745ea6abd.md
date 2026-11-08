nullptr, which means “points nowhere.” Dereferencing a \*nullptr is not allowed (i.e., applying \* or -> to it). Therefore, I first check whether largest still contains nullptr. If so, the current value should definitely be remembered as largest. I could do this with if(largest == nullptr). However, this can be shortened to if(!largest). Together with the size comparison, this becomes if(!largest || \*largest < w). This means that the largest pointer is assigned a new value if it either still contains nullptr or what it points to is smaller than w.

If largest still contains nullptr, the expression to the right of || will not be executed—thanks to short-circuit evaluation, which is explained in Chapter 4, Section 4.3.8, under the heading of the same name.

> > **nullptr**
> >
> > You should never dereference a pointer that can contain nullptr. Check it first to see if it contains a valid address.

If the new value is larger, I get the address of the now last element with &(values.back()) and store this as the new address value in largest. This happens during the program for 20, 30, 81, and at 104.

If I then write a new value to \*largest with \*largest = -999; between the two outputs, I actually overwrite the 104 in vector. You can see the result in the output.

# ## 20.3 Dangers of Aliasing

Did you notice that I secretly inserted the following into Listing 20.1?

```
    values.reserve(50); // Ensure space for 50 values
```

The reason for this is that I need to avoid a danger that arises from being able to access the same value—its memory range—in different ways. That is known as aliasing.

The vector also manages its data somewhere in memory. And one of its properties is that it promises to store them consecutively. However, this means that there might be no space left at the “back” of the vector when you add an element with push_back(). But vector handles this: it requests a new memory range twice as large and copies (or moves) all existing values to the new area. Finally, vector removes the old area.

![](bbox=[0.145, 0.865, 0.37, 0.925])

Figure 20.2 A pointer points into the data of a vector.