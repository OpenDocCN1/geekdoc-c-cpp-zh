# encapsulation

implementation of the type through **encapsulation**. Encapsulation requires that direct access to the data members of a type be restricted to the class methods. Recall that the programmer-defined `Point` class uses the keyword `private` to restrict access to the data members. Encapsulation and a good public interface allow for efficient maintenance and expansion of a type without requiring changes to the applications that depend on the use of the type.

Operator overloading is supported in C++ to allow programmer-defined types to be used as easily as predefined types. We first introduced overloading operators in Chapter 3, where we defined the operator `Point::operator-()` to calculate the distance between two points in a plane. In this section, we look at overloading operators in more detail and introduce the use of the keyword `friend` for overloading the input and output operators `<<` and `>>`.

# # Overloading Operators

Operator overloading allows programmer-defined types to redefine the behavior of an existing operator, with some restrictions. All of the predefined operators in C++, with the exception of four, can be overloaded. It is not possible to define new operators, such as `**`, for exponentiation. The four predefined operators that cannot be overloaded are listed in Table 10.1.

![](bbox=[0.13, 0.34, 0.2, 0.48])

Operators in C++ have a syntax that defines their usage. Unary operators such as `++x` require a single operand, and binary operators such as `x + y` require two operands. When overloading operators in C++, you must adhere to the syntax that defines the operator. Thus, when overloading a binary operator you must provide two operands, and when overloading a unary operator you must provide one operand. To illustrate operator overloading, we will develop a new data type to implement the concept of a pixel.

# ## The Pixel class

+   - picture elements
+   - pixel
+   - red, green, and blue triple
+   - brighten
+   - darken

A digital image can be represented as a collection of **picture elements**. A picture element is a small rectangular region, also referred to as a **pixel**. In the case of a color image, each pixel represents a **red**, **green**, and **blue triple**. Typically, each value in the triple ranges from 0 to 255, where 0 indicates that none of that primary color is present in the pixel and 255 indicates a maximum amount of that primary color. Thus, a pixel displaying the color white will have a value of (255,255,255), and a black pixel will have a value of (0,0,0).

Digital images can be modified by manipulating the pixels that represent an image. For example, we can uniformly **brighten** an image by multiplying each pixel by a small positive value greater than 1, bringing each pixel closer to white. We can uniformly **darken** an image by multiplying each pixel by a positive value less than 1, bringing each pixel closer to black.

| Operator | Description |
| :--- | :--- |
| :: | Scope Resolution Operator |
| . | Dot Operator |
| .* | Pointer to Member Operator |
| ?: | Conditional Operator |