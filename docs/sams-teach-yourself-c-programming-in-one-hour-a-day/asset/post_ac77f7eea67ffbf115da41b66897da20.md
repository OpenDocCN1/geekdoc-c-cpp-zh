
## LESSON 21 Working Memory

## The Bitwise Complement Operator

The bitwise operator covered is the complement operator, ~. This is a unary operator. Its action is to reverse every bit in its operand, changing all 0s to ones, and vice versa. For example, -254 (binary 11111110) evaluates to 1 (binary 00000001).

All the examples in this section have used char variables containing 8 bits. For larger varieties, such as type int and type long, things work exactly the same.

## Bit Fields in Structures

The final bit-related topic is the use of bit fields in structures. In Lesson 11, "Implementing Structures, Unions, and TypeDefs," you learned how to define your own data structures, customizing them to fit your program. By using bit fields, you can accomplish even greater customization and save memory space as well.

A bit field is a structure member that contains a specified number of bits. You can declare a bit field to contain one bit, two bits, or whatever number of bits are required to hold the data stored in the field. What advantage does this provide?

Suppose you are programming an employee database program that keeps records on your company's employees. Many of the items of information that the database stores are of the yes/no variety, such as "Is the employee enrolled in the dental?" or "Did the employee graduate from college?" Each piece of yes/no information can be stored in a single bit, with 1 representing yes and 0 representing no.

Using C's standard data types, the smallest type you could use in a structure is a type char. You could use a type char structure member to hold yes/no data, but 7 of the char's 8 bits would be wasted. By using bit fields, you can store 8 yes/no values in a single char.

Bit fields are not limited to yes/no. Continuing with this database example, imagine that your firm has three health insurance plans. Your database needs to store data about the plan in which each employee is enrolled (if any). You could use 0 to represent no health insurance and the values 1, 2, and 3 to represent the three plans. A bit field containing 2 bits is sufficient because 2 binary bits can represent values of 0 through 3. Likewise, a bit field with 3 bits could hold values in the range 0 through 7, and so on.

Bit fields are named and accessed in the same way as regular structure members. All bit fields have type unsigned int, and you specify the size of the field (in bits) by following the member name with a colon and the number of bits. To define a structure with a 1-bit member named dental, another 1-bit member named college, and a 2-bit member named health, you write the following:

```c
struct emp_data
{
    unsigned dental : 1;
    unsigned college : 1;
    unsigned health : 2;
};
```

The ellipsis (...) indicates space for other structure members. The members can be fields or fields made up of regular data types. Note that bit fields must be placed first in the structure definition before any non-bit field structure members. To access the bit fields, use the structure member operator as you do with any structure member. For the example, you can expand the structure definition to something more useful:

```c
struct emp_data
{
    unsigned dental : 1;
    unsigned college : 1;
    unsigned health : 2;
    char fname[20];
    char lname[20];
    char sname[10];
};
```

You can declare an array of structures:

```c
struct emp_data workers[100];
```

To assign values to the first array element, write something like this:

```c
workers[0].dental = 1;
workers[0].college = 0;
workers[0].health = 2;
strcpy(workers[0].fname, "Mildred");
```

Your code would be clearer, of course, if you used symbolic constants YES and NO with values of 1 and 0 when working with 1-bit fields. In any case, you treat each bit field as a small, unsigned integer with the given number of bits. The range of values that can be assigned to a bit field with n bits is from 0 to $2^n-1$. If you try to assign an out-of-range value to a bit field, the compiler won't report an error, but you will.

## LESSON 21 Working Memory

| DO | DON'T |
| :--- | :--- |
| Use symbolic constants YES and NO with values of 1 and 0 when working with 1-bit fields. | The range of values that can be assigned to a bit field with n bits is from 0 to $2^n-1$. If you try to assign an out-of-range value to a bit field, the compiler won't report an error, but you will. |

## Summary

Today's lesson covered the use of bit fields in structures. You learned how to define bit fields to save memory space. You also learned how to name and access them just like regular structure members. Remember that bit fields must be placed at the beginning of the structure.

## Q&A

- What's the advantage of `memset()`, `memcpy()`, and `memmove()` functions?
Why can't I use a loop with assignment statement to initialize or copy memory?
You can use a loop with assignment statement to initialize memory in some cases. In fact, this is the only way to do it—for example, setting all elements of a `float` array to `1.23`. In other situations, however, the memory will not have been assigned, and the `mem()` functions are your choice.

- When will I use the shift operators and the bitwise operators?
A common use for these operators is when a program is interacting directly with hardware—a task that often requires specific bit patterns to be generated and interpreted. This topic is beyond the scope of this book. Even if you need to manipulate hardware directly, you can use the shift operators, in circumstances, to divide or multiply integer values by powers of two.

- What happens if I need to resize memory?
You can overwrite the string as long as the new string is equal to or smaller than the original. However, if the new string is bigger, you call `realloc()`.

- Why would I ever need to free memory?
Some systems automatically return memory when programs end.

- Do I really gain that by using bit fields?
Yes, you can gain a bit with bit fields. (Pun intended!) Consider a circumstance similar to the example in this chapter in a file contains information of a survey. People are asked to answer `TRUE` or `FALSE` to the questions. If you ask 100 questions of 10,000 people and store each answer as a type `char` as T or F, you will need 10,000 × 100 bytes of storage (because a character is 1 byte). This is 1 million bytes. If you use bit fields instead and allocate 1 bit for each answer, you need 10,000 × 100 bits. Because 1 byte holds 8 bits, this amounts to 130,000 bytes of data, which is significantly less than 1 million bytes.
