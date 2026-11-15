
- 26. Modify program chapter 9_13 to insert all words into the list, then call the member function unique() to remove duplicate words.

- 27. Modify program chapter 9_13 to keep a count of how many times each unique word appears in the text file.

- 28. Write a function that assigns the value v to the first n elements of the array x. Use the prototype:

```
void assignV(double *x, int n, double v);
```

- 29. Write a function that assigns a random value to the first n elements of the array x. Use the prototype:

```
void assignRandom(double *x, int n );
```

![](img/0235a4ea835dc4575bd036e024a533b3_556_0.png)

Source: Garry Gay/Alamy Stock Photo

## ENGINEERING CHALLENGE: Artificial Intelligence

Artificial Intelligence (AI) is an intriguing area of science that focuses on creating intelligent machines that have the ability to “think.” Research in the areas of robotics, cognitive science, language, computing, and sensory perception have advanced the creation of intelligent machines. Today, software exists that can conduct a dialog with human clients, beat a world-class chess player, and aid in the diagnosis of disease. Virtual pets are available that “learn” about their environment and respond to their owners. The intelligent software that exists today is only a hint of what is to come.

## ADVANCED TOPICS

### CHAPTER OUTLINE

- Objectives
- 10.1 Data Abstraction
- 10.2 Building C++ Solutions with IDEs: Xcode Image Files
- 10.3 Binary File Input and Output
- 10.4 Problem Solving Applied: Color Image Processing
- 10.5 Recursion
- 10.6 Generic Programming
- 10.7 Inheritance
- 10.8 virtual Methods
- 10.9 Problem Solving Applied: Iterated Prisoner's Dilemma
- Summary, Key Terms, C++ Statement Summary, Style Notes, Debugging Notes, Problems

### OBJECTIVES

In this chapter, we develop problem solutions containing:

- binary data files
- overloaded operators
- image processing examples
- recursive member functions
- templates
- class hierarchies
- an implementation of the iterated prisoner's dilemma game

### 10.1 Data Abstraction

In real-world applications, it is very common to work with concepts that are not available as built-in or predefined data types. Problem solutions to real-world applications require multiple programmers working separately on different aspects of a solution. In these situations, an object-oriented approach to the design and implementation of a solution is desirable. Defining a new type to represent a concept ensures that all programmers are working with the same physical definition for the concept and adhering to the same rules of operation, thus reducing the potential for errors and increasing productivity. Programmer-defined types can also be used as building blocks to define more complex concepts.

The C++ programming language supports object-oriented programming through the use of programmer defined types, or **data abstraction**. C++ supports the use of classes to define new types that can be used as easily as built-in types and receive nearly as much compiler support as built-in types. A well-designed type provides a good public interface and hides the encapsulation implementation of the type through **encapsulation**. Encapsulation requires that direct access to the data members of a type be restricted to the class methods. Recall that the programmer-defined `Point` class uses the keyword `private` to restrict access to the data members. Encapsulation and a good public interface allow for efficient maintenance and expansion of a type without requiring changes to the applications that depend on the use of the type.

Operator overloading is supported in C++ to allow programmer-defined types to be used as easily as predefined types. We first introduced overloading operators in Chapter 3, where we defined the operator `Point::operator-()` to calculate the distance between two points in a plane. In this section, we look at overloading operators in more detail and introduce the use of the keyword `friend` for overloading the input and output operators `<<` and `>>`.

## Overloading Operators

Operator overloading allows programmer-defined types to redefine the behavior of an existing operator, with some restrictions. All of the predefined operators in C++, with the exception of four, can be overloaded. It is not possible to define new operators, such as `**`, for exponentiation. The four predefined operators that cannot be overloaded are listed in Table 10.1.

![](img/0235a4ea835dc4575bd036e024a533b3_558_0.png)

Operators in C++ have a syntax that defines their usage. Unary operators such as `++x` require a single operand, and binary operators such as `x + y` require two operands. When overloading operators in C++, you must adhere to the syntax that defines the operator. Thus, when overloading a binary operator you must provide two operands, and when overloading a unary operator you must provide one operand. To illustrate operator overloading, we will develop a new data type to implement the concept of a pixel.

### The Pixel class

- picture elements
- pixel
- red, green, and blue triple
- brighten
- darken

A digital image can be represented as a collection of **picture elements**. A picture element is a small rectangular region, also referred to as a **pixel**. In the case of a color image, each pixel represents a **red**, **green**, and **blue triple**. Typically, each value in the triple ranges from 0 to 255, where 0 indicates that none of that primary color is present in the pixel and 255 indicates a maximum amount of that primary color. Thus, a pixel displaying the color white will have a value of (255,255,255), and a black pixel will have a value of (0,0,0).

Digital images can be modified by manipulating the pixels that represent an image. For example, we can uniformly **brighten** an image by multiplying each pixel by a small positive value greater than 1, bringing each pixel closer to white. We can uniformly **darken** an image by multiplying each pixel by a positive value less than 1, bringing each pixel closer to black.

| Operator | Description |
| :--- | :--- |
| :: | Scope Resolution Operator |
| . | Dot Operator |
| .* | Pointer to Member Operator |
| ?: | Conditional Operator |

When we multiply a pixel by a value, we want to multiply each of the three color values of the pixel—the red value, the green value, and the blue value—by the same amount, and we would like to do this in a single multiplication using the multiplication * operator. Thus, we will overload the multiplication operator when we define our Pixel class.

smoothing

neighborhood

Another modification we can perform on a digital image is called smoothing. To smooth an image, we replace each pixel with an average of the surrounding pixels. The number of surrounding pixels we choose to include is referred to as the neighborhood. The size of the neighborhood determines the degree of smoothing: the larger the neighborhood, the more dramatic the smoothing. For example, we can uniformly smooth an image by replacing each pixel, except the pixels on the boundaries of the image, with an average of four surrounding pixels: the pixel above, the pixel below, the pixel to the right, and the pixel to the left. To calculate an average, we need to sum the pixel values and divide by the number of pixels. When we sum two pixels, we want to add the red values, the green values, and the blue values of the two pixels. When we divide a pixel by a value, we want to divide the red value, the green value, and the blue value by the same value. Thus, we will overload the addition operator and the division operator.

We have identified the attributes of a pixel as a red, green, and blue triple, and we have defined three arithmetic operations (addition, multiplication, and division) required to modify the value of a pixel. We will now implement a Pixel class, using the class declaration provided below.

```
/**-------------------------------------------------------------**/
/* Pixel class declaration.                                      */
/* File name: Pixel.h                                            */
/* This class implements the concept of a pixel                  */
/*                                                               */
#include <iostream> //Required for istream, ostream
using namespace std;
class Pixel
{
   public:
      //Constructors
      Pixel(); //Default
      Pixel(unsigned ); //Gray scale
      Pixel(unsigned,unsigned,unsigned ); //Full color range
      //Overloaded operators.
      //Addition.
      Pixel operator+(const Pixel& p) const;
      //Multiplication of a Pixel by a floating point value.
      Pixel operator*(double v) const;
      //Division of a Pixel by an integer value.
      Pixel operator/(unsigned v) const;
      //Input operator.
      friend istream& operator >> (istream& in, Pixel& p);
```
