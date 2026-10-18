ordinary function to a template by replacing some type names with a type parameter. There are two advantages to this method. First, when you are defining the ordinary function you are dealing with a much more concrete case, which makes the problem easier to visualize. Second, you have fewer details to check at each stage; when worrying about the algorithm itself, you need not concern yourself with template syntax rules.

# PITFALL Using a Template with an Inappropriate Type²

You can use a template function with any type for which the code in the function definition makes sense. However, all the code in the template function must make sense and must behave in an appropriate way. For example, you cannot use the swapValues template (Display 17.1) with the type parameter replaced by a type for which the assignment operator does not work at all or does not work “correctly.”

As a more concrete example, suppose that your program defines the template function swapValues as in Display 17.1. You cannot add the following to your program:

```
int a[10], b[10];
<some code to fill arrays>
swapValues(a, b);
```

This code will not work, because assignment does not work with array types.

# SELF-TEST EXERCISES

+   5. Display 7.10 shows a function called search, which searches an array for a specified integer. Give a function template version of search that can be used to search an array of elements of any type. Give both the function declaration and the function definition for the template. (Hint: It is almost identical to the function given in Display 7.10.)

+   6. In Practice Program 8 of Chapter 4 you were asked to overload the abs function so that the name abs would work with several of the built-in types that had been studied at the time. Compare and contrast function overloading of the abs function with the use of templates for this purpose in Self-Test Exercise 2.

²The example in this Pitfall section uses arrays. If you have not yet covered arrays (Chapter 7), you should skip this Pitfall section and return after covering arrays.