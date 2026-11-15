
```
// Position iter at beginning of list.
iter = wordlist.begin();
while(iter != wordlist.end())
{
    out_stream << setw(20) << (*iter);
    iter++;
    counter++;
    if(counter%columns == 0)
    {
        out_stream << endl;
    }
}
```

## 5. TESTING

If we use the text from the hand example, we get the following information written to a data file:

There are 13 distinct words in the text file;
a concordance an alphabetical
concordance file in
is list of
text the unique
words

## SUMMARY

In this chapter, we looked at the relationships between the value stored in an object, the identifier assigned to an object, and the address of the memory location used to store the value of an object. A new pointer data type was defined that can be used to hold the address of another object. Examples were presented to demonstrate the use of pointers to reference array elements and character strings. The process of dynamic memory allocation was defined. The operators new and delete were examined, and the vector class was revisited as an alternative to dynamic memory allocation. Data structures, including linked list, stacks and queues, were discussed, with examples that utilize the list, stack, and queue classes.

## Key Terms

- address indirection
- address operator
- linked data structures
- container
- list
- deallocation
- pointer
- dereference
- queue
- dynamic data structures
- stack
- dynamic memory allocation

## C++ Statement Summary

Pointer declaration:

General Form:

data type *identifier [,*identifier];

Example:

int *ptr_1;
double a, *ptr_2=&a;

Dynamic memory allocation:

General Form:

pointer_object = new datatype;

Example:

ptr = new double;

Deallocation of dynamic memory:

General Form:

delete pointer_object;

Dynamic array memory allocation:

arr_ptr = new double[100];

Deallocation of dynamic array:

General Form:

delete []pointer_object;

- Notes
- 1. Choose identifiers for pointers that clearly indicate that the identifiers are associated with pointer objects.
- 2. If a pointer is not initially assigned to a memory location, assign it the literal value nullptr to indicate that it does not point to any object.

- Notes
- 1. Be sure that a program initializes an object before using its value in other statements.
- 2. Be sure that a pointer object is initialized before it is used to reference a value.
- 3. The actual parameter that corresponds to a pointer argument in a function must be an address or a pointer.

## Problems

### Exam Practice!

### True/False Problems

Indicate whether the following statements are true (T) or false (F).

- 1. Both the address operator and the indirection operator are unary operators. T F
- 2. A pointer provides an indirect means of accessing the value of a particular data item. T F
- 3. An object must always be declared and initialized before a pointer can point to it. T F
- 4. The memory locations given to dynamic memory space are determined when the program is compiled. T F

### Multiple-Choice Problems

Circle the letter for the best answer to complete each statement or for the correct answer to each question.

- 5. A location in memory
- (a) is reserved whenever an object is declared.
- (b) is reserved when an object is used in a program.
- (c) can hold several different values at the same time.
- (d) cannot be reused once it is assigned a value.

- 6. A pointer object
- (a) contains the data stored at a location in memory.
- (b) contains the address of a memory location.
- (c) can be used in input statements, but not output statements.
- (d) can be changed to different values in both input and output statements.

- 7. How would you assign to the object name the value of an object referenced by the pointer a?
- (a) a = *name;
- (b) name = &a;
- (c) a = *name;
- (d) name = *a;

- 8. Assume that a and b are pointers to integers and that a points to the object name.
- What is the effect of the statement
- b = a;
- (a) The value of name is copied into b.
- (b) The memory address stored in a is copied into b.
- (c) The memory address stored in b is copied into a.
- (d) The pointer a is now pointing to a different object.

### Memory Snapshot Problems

9. Give the corresponding snapshot of memory after the following set of statements is executed:

```
double name, x(20.5);
double *a = &x;
name = *a;
```

Assume the address of name is 10 and the address of x is 14. (That is, name is stored in memory location 10, and x is stored in memory location 14.) Problems 10–13 refer to the following statements:

```
int i1, i2;
int *p1, *p2;
i1 = 5;
p1 = &i1;
p2 = *p1/2 + 10;
p2 = p1;
```

- 10. What is the value of i1?
- 11. What is the value of i2?
- 12. What is the value of *p1?
- 13. What is the value of *p2?

### Vector Functions. These problems develop functions for manipulating values within a vector.

14. Write a function that creates a vector of size n, with each element assigned the value v. Assume that the function prototype statement is

```
void assign_n(vector <double> &x, int n, double v);
```

15. Write a function that creates a vector of n random numbers between a and b. Assume that the function prototype statement is

```
void assign_random(vector <int> &x, int n, int a, int b);
```

16. Write a function that computes the sum of a vector. Assume that the function prototype statement is

```
int v_sum(vector<int> x);
```

17. Write a function that replaces values in a vector with their absolute values. Assume that the function prototype statement is

```
void v_abs(vector<int>&x);
```

### Character Functions: Pattern Recognition.

Many areas of engineering use problem solutions in which we search for a specific pattern of information in a signal. Problems 17–24 develop a set of functions for this purpose.

- 18. Write a function that receives a pointer to a character string and a character. The function should return the number of times that the character occurred in the string. Assume that the function has the prototype statement

int charcnt(char *ptr, char c);

- 19. Write a function that receives a pointer to a character string and returns the number of repeated characters that occur in the string. For example, the string “Mississippi” has three repeated characters. Do not count repeated blanks in the string. If a character occurs more than two times, it should still only count as one repeated character; thus, “hisssss” would have only one repeated character. Assume that the function has the prototype statement

int repeat(char *ptr);

- 20. Rewrite the function from Problem 19 so that each pair of characters is counted as a repeat. Thus, the string “hisssss” would have four repeated characters. Assume that the function has the prototype statement

int repeat2(char *ptr);

- 21. Write a function that receives pointers to two character strings and returns a count of the number of times that the second character string occurs in the first character string. Do not allow overlap of the occurrences. Thus, the string “110101” contains only one occurrence of “101.” Assume that the function has the prototype statement

int overlap(char *ptr1, char *ptr2);

- 22. Rewrite the function from Problem 21 so that overlap of the occurrences of the second string in the first string is allowed. Thus, the string “110101” contains two occurrences of “101.” Assume that the function has the prototype statement

int overlap(char *ptr1, char *ptr2);

- 23. Rewrite the function in Problem 19 using the string class instead of C-style strings. Assume that the function has the prototype statement

int repeat(string);

- 24. Rewrite the function in Problem 20 using the string class instead of C-style strings. Assume that the function has the prototype statement

int repeat2(string);

- 25. Rewrite the function in Problem 21 using the string class instead of C-style strings. Assume that the function has the prototype statement

int pattern(string, string);
