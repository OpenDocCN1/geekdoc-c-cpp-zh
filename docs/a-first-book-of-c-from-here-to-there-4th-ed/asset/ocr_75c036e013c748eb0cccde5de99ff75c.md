# Point of Information

**Pointers Versus References**

The distinguishing characteristic of a pointer, as a formal parameter or variable, is that every pointer contains a value that’s an address. Whereas a pointer is a variable argument with an address as its content, a reference is an address. Therefore, a reference can be thought of as a named constant, with the constant being a valid memory address.

From an advanced programming viewpoint, pointers are more flexible than references because a pointer’s contents can be manipulated in much the same manner as any other variable’s value. The disadvantage of pointers is that their flexibility makes them more complicated to understand and use than references. Because references (as both variables and arguments) can be used only as named addresses, they’re easier to use. Therefore, when the compiler encounters a reference, it dereferences the address automatically to obtain the contents of the address. This isn’t the case with pointers. If you use a pointer’s name, as noted previously, you access the pointer’s contents. To dereference the address stored in a pointer correctly, you must use C++’s indirection operator, `*`, in front of the pointer name. This operator informs the compiler that what you want is the item whose address stored in the pointer variable.

can be written as follows:

```
void Date::showDate()
{
    cout << setfill('0')
         << setw(2) << this->month << '/'
         << setw(2) << this->day << '/'
         << setw(2) << this->year % 100;
    return;
}
```

Clearly, using the `this` pointer in this manner is unnecessary and simply clutters up `showDate()`’s code. At times, however, an object must be returned from a method. In many of these situations, one of which is discussed in the next section, the address stored in the `this` pointer must be used.

# The Assignment Operator Revisited

Section 11.1 showed a simple assignment operator method that has the following prototype:

```
void operator=(const Date &);
```

The drawback of the method this prototype declares is that it returns no value. Consequently, multiple assignments, such as `a = b = c`, aren’t possible. The reason is that the right-to-left association of the `=` operator causes the assignment `b = c` to be made first. This assignment results in a void being returned from this expression. Attempting to assign this data type to the Date object `a` results in an error.