![](bbox=[0.06, 0.07, 0.9, 0.62])

FIGURE 1.4 From code to instructions.

# The Common Type System Explained

Types are the way of life in the world of the CLR. They define the way libraries and programs are organized and how interactions between components can be realized. Assemblies are containers for such types.

Let's explore the merits of types in some more detail and look at the various kinds of types supported by the runtime. Don't worry about the C# syntax for now; we cover that extensively as we move along.

# What's Type Safety?

To enforce code to deal with types in a correct manner, the CLR guarantees type safety. This ensures objects can only be accessed in a manner that's consistent with the object's type contract. Types consist of two things: the data that's contained by objects of the type (for example, a customer's name and credit balance) and the operations you can perform on that data (for example, DiscountPrice on a Product).

To illustrate type-unsafe operations, assume you were able to treat an object of type Customer as if it were of type Product. Then, what would it mean to perform an operation DiscountPrice to the customer object? Maybe you'd be changing the customer's credit balance. This is clearly an unsafe thing to do. Similarly, arbitrary memory access is an