The result of this operation is illustrated in Figure 4-5.

![](bbox=[0.22, 0.13, 0.75, 0.33])

Figure 4-5

You can use the operator & to obtain the address of any variable, but you need a pointer of the appropriate type to store it. If you want to store the address of a double variable for example, the pointer must have been declared as type double*, which is type ‘pointer to double’.

# Using Pointers

Taking the address of a variable and storing it in a pointer is all very well, but the really interesting aspect is how you can use it. Fundamental to using a pointer is accessing the data value in the variable to which a pointer points. This is done using the indirection operator, *.

# The Indirection Operator

You use the indirection operator, *, with a pointer to access the contents of the variable that it points to. The name ‘indirection operator’ stems from the fact that the data is accessed indirectly. It is also called the de-reference operator, and the process of accessing the data in the variable pointed to by a pointer is termed de-referencing the pointer.

One aspect of this operator that can seem confusing is the fact that you now have several different uses for the same symbol, *. It is the multiply operator, it also serves as the indirection operator, and it is used in the declaration of a pointer. Each time you use *, the compiler is able to distinguish its meaning by the context. When you multiply two variables, A*B for instance, there’s no meaningful interpretation of this expression for anything other than a multiply operation.

# Why Use Pointers?

A question that usually springs to mind at this point is, “Why use pointers at all?” After all, taking the address of a variable you already know and sticking it in a pointer so that you can de-reference it seems like an overhead you can do without. There are several reasons why pointers are important.

As you will see shortly, you can use pointer notation to operate on data stored in an array, which often executes faster than if you use array notation. Also, when you get to define your own functions later in the book, you will see that pointers are used extensively for enabling access within a function to large