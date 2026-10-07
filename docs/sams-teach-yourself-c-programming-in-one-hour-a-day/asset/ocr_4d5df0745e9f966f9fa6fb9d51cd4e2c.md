# Analysis

This program is a simplistic version of what could be done with a union. This program provides a way of storing multiple data types in a single storage space. The generic_tag structure lets you store a character, an integer, or a floating-point number within the same area. This area is a union called shared that operates just like the examples in Listing 11.7. Notice that the generic_tag structure also adds an additional field type. This field is used to store information of the variable contained in shared type prevents using shared from the wrong way, thus helping to avoid erroneous data such as presented in Listing 11.7.

A formal look at the program shows that lines 5, 6, and 7 define constants CHARACTER, INTEGER, and FLOAT. These are used in the program to make the listing readable. Line 9 through 16 define a generic_tag structure that will be used. Line 18 presents a prototype for the void function print_function(). The structure var is declared in line 22 and is initialized to hold a value in 24 and 25. A call to print_function() on line 26 makes the value printed. Lines 28 through 30 and 32 through 34 repeat this process with other values.

The print_function() is the heart of the listing. Although this function is used to print the value from a generic_tag variable, a similar function could have been used to initialize it. print_function() evaluates the type variable in order to print a statement with the appropriate type variable. This prevents getting erroneous data such as in Listing 11.7.

| DO | DON'T |
|---|---|
| DO remember union member is being used. If you are in a member of one type and then try to use a different type, you can get unexpected results. | DON'T try to initialize more than the first union member. <br> DON'T forget that the size of a union is equal to its largest member. |

# Creating Synonyms for Structures with typedef

You can use the typedef keyword to create a synonym for a structure or union type. For example, the following statements define coord as a synonym for the indicated structure:

```
typedef struct {
  int x;
  int y;
} coord;
```