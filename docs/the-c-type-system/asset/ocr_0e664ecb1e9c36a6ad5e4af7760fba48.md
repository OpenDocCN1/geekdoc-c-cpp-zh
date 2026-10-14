# 5

# TYPES OF EQUALITY

![](bbox=[0.14, 0.48, 0.32, 0.62])

Programs frequently compare variables to see if their values are equal, although this operation is often overlooked because it’s done implicitly. Every type inherits the Equals method from the object base class, so given any two values x and y, the expression x.Equals(y) is always valid.

C# also provides ==, or the equals-equals operator, for explicitly checking equality of two values. Using == for comparisons differs from using the Equals method in multiple ways. In this chapter, we’ll look at why C# supports two techniques for equality comparison and how each is affected by the differences between types.

We’ll explore the following:

+   - How the differences between comparisons using the Equals method versus == affect our programs
+   - What support the compiler provides for comparisons, and what we must provide ourselves
+   - Why equality comparisons and hash codes are so closely related