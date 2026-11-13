the asterisk with the data type (int) rather than with the parameter name (i_ptr)—although the compiler will accept the asterisk in either position. The reason for the placement with the data type is to emphasize that the “complete type” of the parameter is “an integer pointer.”

The only purpose of make_it_42 is to show what happens when a value parameter is a pointer. Notice that the body of the function does not actually change i_ptr; it changes only the integer that i_ptr points to. Let’s examine a program that calls make_it_42. The program declares a pointer to an integer, allocating memory for the pointer to point to, and calls make_it_42:

```
int *main_ptr;
main_ptr = new int;
Now main_ptr is pointing
to a newly allocated integer.
Next, we call make_it_42 with
main_ptr as the actual parameter.
make_it_42(main_ptr);
```

![](bbox=[0.48, 0.333, 0.74, 0.393])

As with any value parameter, the actual argument provides the initial value for the formal parameter. In the example, main_ptr provides the initial value for the formal parameter i_ptr of the make_it_42 function. This means that the parameter i_ptr will point to the same place that main_ptr is already pointing to. At the start of the function’s execution, we have this situation:

The argument, main_ptr, provides the initial value for the parameter i_ptr.

![](bbox=[0.48, 0.513, 0.68, 0.623])

Within the make_it_42 function, we have the assignment *i_ptr = 42. The assignment places 42 in the location that i_ptr points to, as shown here:

In the body of make_it_42, the assignment statement ‘i_ptr = 42 places 42 in the location that i_ptr points to.

![](bbox=[0.48, 0.68, 0.68, 0.793])