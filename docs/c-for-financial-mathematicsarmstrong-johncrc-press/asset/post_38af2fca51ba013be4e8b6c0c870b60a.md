
This function above integrates the payoff function of an option between the range *a* and *b*. We have to store the member variable using a reference because you cannot store polymorphic variables by value. Storing data in member variables by reference can be dangerous, because the data referred to may be deleted before the object holding the reference is deleted. This would cause the program to behave badly and perhaps crash. In this case, the code will delete the variable *integrand* from memory the moment *integratePayoff* returns. So there should be no danger of *option* being deleted before *integrand* is deleted.

There is an neater notation called *lambda functions* which can be used to create local classes. We will revisit the example of writing an integrator in Chapter 19 and show how the use of lambda classes simplifies the code.

We should also add that the rectangle rule is not the best integration method to use. You probably already know of Simpson's rule. An even more interesting technique for one-dimensional numerical integration is called Gaussian quadrature. Numerical libraries such as the Gnu scientific library contain sophisticated integration routines that you should use in practice.

## Exercises

- 10.6.1. Write classes `DigitalCallOption` and `DigitalPutOption`. Price them using the `MonteCarloPricer`. See Appendix A if you do not recall what a digital option is.
- 10.6.2. Write a class `NormalPDF` and compute its integral from -1.96 to 1.96.
- 10.6.3. Write a function `integralToInfinite` that uses integration by substitution to transform an infinite integral to one the function `integral` can compute.
- 10.6.4. Test the `normcdf` function against numerical integration of the pdf of the normal distribution.
- 10.6.5. Write a function `differentiateNumerically` that can differentiate any `RealFunction`.
- 10.6.6. Write an interface `Cipher` and provide at least two implementations of your choice. Write a single function `void testCipher(Cipher& toTest)` that can test any Cipher works correctly.
- 10.6.7. Draw a UML diagram for your Cipher classes.
- 10.6.8. Write a class `RectangleRulePricer` which can price a Path-DependentOption using the numerical integration routines written in the earlier exercises. Use Equation (A.3) to compute the probability density function for the log of the stock price. Check your solution works with a **CallOption**. This gives a numerical test of the derivation of Equation (A.6).
- 10.6.9. Design an interface called `ContinuousTimeOption`. It should have a function `payoff` which takes a vector of stock prices and a vector of times at which the price occurred. This should return the payoff that would have occurred if the stock price had varied linearly between the time points. (Obviously we can't actually supply the stock price at an infinite number of points). The `ContinuousTimeOption` should also have a function called `getMaturity()`. Write an implementation of `ContinuousTimeOption` called `KnockOutCallOption`. Add a function to `MonteCarloPricer` which can approximate the price of any `ContinuousTimeOption` given a finite number of time steps.
- 10.6.10. Show that you could use `if` statement to write an `integrate` function which can numerically integrate any of the following specific functions (but no others):
  - $\sin(x)$
  - $\cos(x)$
  - $\exp(x)$
  
  Explain why this is not a good design. Use this to explain why using an `if` statement to decide how to price puts and calls differently is not as powerful as using an interface.

## 10.7 Summary

- By defining interfaces we can write code that will work with inputs we haven't thought of yet.
- This is essential to writing real code for the financial industry where new products are invented every day.
- Interfaces are common in everyday life. Cars, doors, guitars, and plug sockets are all familiar examples of things that are easy to use because they implement a well-known interface.
- Learning how to use interfaces is the most important skill in object-oriented design.

# Chapter 11

# Arrays, Strings, and Pointers

One useful way to view C++ is as a collection of languages:

- (i) the C language;
- (ii) an object-oriented programming language;
- (iii) a template programming language.

This chapter is about some of the C language aspects of C++. We have ignored them so far, because you should focus your efforts on the object-oriented features of C++. Similarly we will not discuss the template programming features until Chapter 17.

Pointers are a central feature of the C language. They are a tool for directly manipulating computer memory. You will not find them in a more modern pure object-oriented programming language like Java. The feature is omitted from other languages because pointer-based programs are typically harder to understand than object-oriented programs.

Most of what you learn in this chapter you should never use directly. The only thing you need to use is `shared_ptr`. We will discuss this towards the end of the chapter. Unfortunately, to understand `shared_ptr` you must first understand ordinary pointers.

There are three other motivations for studying the material in this chapter.

- (i) The first is that C++ was originally designed for people with C programming experience. So some C++ code is designed to be intuitive to use if you have experience with C pointers. If you don't study pointers, you will find things like the C++ standard library very unintuitive.
- (ii) The second is that job interviewers may assume that you know C and so may ask some trick questions about pointers, so it is good to be prepared!
- (iii) The third is that to write maximally efficient C++ programs it can be helpful to manage memory consciously. Pointers are a tool for direct memory manipulation.

Because this chapter and the next are more about C programming than object-oriented programming, we've temporarily abandoned developing FM-Lib for this chapter. Instead the project `PointerExamples.zip` contains all code for this chapter.

As you will see, there is just one large main.cpp file which contains all the various examples in sequence. The main method just calls various test functions in sequence. Some of the tests have been commented out because they illustrate what you *shouldn't* do. If you include them, the program will probably crash.

## **11.1 Arrays, the C alternative to vector**

The code below shows how you create an array consisting of 5 integers in C++. An array is a bit like a vector in that it contains a sequence of values, but as we will see, arrays are not as useful as vectors.

```cpp
// Create an uninitialised array of length 5
int myArray[5];
for (int i=0; i<5; i++) {
    cout<<"Entry "<<i<<"=";
    cout<<myArray[i];
    cout<<"\n";
}
```

This code creates an array of 5 integers, without initialising it. It then runs through the entries and prints them out. Since we haven't initialised the values, it will print out some random integers.

Note the similarities with vector. Just as with vector, we use [] to access the entries. Just as with vector, the entries start at 0.

The one difference you can spot is that we are not using the *size()* function. This is because a C array has no size function. Actually, you can use the *sizeof* operator and write *sizeof(myArray)/sizeof(int)* where we have written 5. This would be better programming style, but I've avoided it because it is less readable when you are new to arrays.

To create an array that is initialised one proceeds as follows:

```cpp
// Create an initialised array
int myArray[] = {1, 1, 2, 3, 5};
for (int i=0; i<5; i++) {
    cout<<"Entry "<<i<<"=";
    cout<<myArray[i];
    cout<<"\n";
}
```

Simply specify the values in a comma-separated list between curly brackets. Notice that if we provide a list of values, we no longer have to specify the length of the array when we create it.
