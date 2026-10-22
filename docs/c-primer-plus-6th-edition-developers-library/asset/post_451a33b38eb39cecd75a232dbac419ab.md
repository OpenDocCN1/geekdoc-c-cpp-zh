
Recall that, beginning with the ANSI C standard, C concatenates string literals if they are separated by nothing or by whitespace. For example,

```
char greeting[50] = "Hello, and"" how are" " you"
                  " today!";
```

is equivalent to this:

```
char greeting[50] = "Hello, and how are you today!";
```

If you want to use a double quotation mark within a string, precede the quotation mark with a backslash, as follows:

```
printf("\"Run, Spot, run!\" exclaimed Dick.\n");
```

This produces the following output:

```
"Run, Spot, run!" exclaimed Dick.
```

Character string constants are placed in the static storage class, which means that if you use a string constant in a function, the string is stored just once and lasts for the duration of the program, even if the function is called several times. The entire quoted phrase acts as a pointer to where the string is stored. This action is analogous to the name of an array acting as a pointer to the array's location. If this is true, what kind of output should the program in Listing 11.2 produce?

## Listing 11.2 The strptr.c Program

```
/* strptr.c -- strings as pointers */
#include <stdio.h>
int main(void)
{
    printf("%s, %p, %c\n", "We", "are", *"space farers");
    
    return 0;
}
```

The %s format should print the string We. The %p format produces an address. So if the phrase "are" is an address, then %p should print the address of the first character in the string. (Pre-ANSI implementations might have to use %u or %lu instead of %p.) Finally, *"space farers" should produce the value to which the address points, which should be the first character of the string "space farers". Does this really happen? Well, here is the output:

```
We, 0x100000f61, s
```

```
int n = 8;
char cookies[1];    // valid
char cakes[2 + 5];  // valid, size is a constant expression
char pies[2*sizeof(long double) + 1];  // valid
char crumbs[n];     // invalid prior to C99, a VLA after C99
```

The name of a character array, like any array name, yields the address of the first element of the array. Therefore, the following holds:

```
char car[10] = "Tata";
car == &car[0] , *car == 'T', and *(car+1) == car[1] == 'a'
```

Indeed, you can use pointer notation to set up a string. For example, Listing 11.1 uses the following declaration:

```
const char * pt1 = "Something is pointing at me.";
```

This declaration is very nearly the same as this one:

```
const char ar1[] = "Something is pointing at me.";
```

The declarations amount to saying that both pt1 and ar1 are addresses of strings. In both cases, the quoted string itself determines the amount of storage set aside for the string. Nonetheless, the forms are not identical.

## Array Versus Pointer

What is the difference, then, between an array and a pointer form? The array form (ar1[]) causes an array of 29 elements (one for each character plus one for the terminating '\0') to be allocated in the computer memory. Each element is initialized to the corresponding character of the string literal. Typically, what happens is that the quoted string is stored in a data segment that is part of the executable file; when the program is loaded into memory, so is that string. The quoted string is said to be in static memory. But the memory for the array is allocated only after the program begins running. At that time, the quoted string is copied into the array. (Chapter 12, "Storage Classes, Linkage, and Memory Management," will discuss memory management more fully.) Note that, at this time, there are two copies of the string. One is the string literal in static memory, and one is the string stored in the ar1 array.

Hereafter, the compiler will recognize the name ar1 as a synonym for the address of the first array element, &ar1[0]. One important point here is that in the array form, ar1 is an address constant. You can't change ar1, because that would mean changing the location (address) where the array is stored. You can use operations such as ar1+1 to identify the next element in an array, but ++ar1 is not allowed. The increment operator can be used only with the names of variables (or, more generally, modifiable lvalues), not with constants.

The pointer form (*pt1) also causes 29 elements in static storage to be set aside for the string. In addition, once the program begins execution, it sets aside one more storage location for the pointer variable pt1 and stores the address of the string in the pointer variable. This variable

This produces the following output:

```
I love Millie!
```

Suppose you want head to agree with heart. You can say

```
head = heart;  /* head now points to the array heart */
```

This makes the head pointer point to the first element of the heart array.

However, you cannot say

```
heart = head;  /* illegal construction */
```

The situation is analogous to x = 3; versus 3 = x;. The left side of the assignment statement must be a variable or, more generally, a modifiable lvalue, such as *p_int. Incidentally, head = heart; does not make the Millie string vanish; it just changes the address stored in head. Unless you've saved the address of "I love Millie!" elsewhere, however, you won't be able to access that string when head points to another location.

There is a way to alter the heart message—go to the individual array elements:

```
heart[7] = 'M';
```

or

```
*(heart + 7) = 'M';
```

The elements of an array are variables (unless the array was declared as const), but the name is not a variable.

Let's go back to a pointer initialization that doesn't use the const modifier:

```
char * word = "frame";
```

Can you use the pointer to change this string?

```
word[1] = 'l';  // allowed??
```

Your compiler may allow this, but, under the current C standard, the behavior for such an action is undefined. Such a statement could, for example, lead to memory access errors. The reason is that, as mentioned before, a compiler can choose to represent all identical string literals with a single copy in memory. For example, the following statements could all refer to a single memory location of string "Klingon":

```
char * p1 = "Klingon";
p1[0] = 'F';     // ok?
printf("Klingon");
printf(": Beware the %s!\n", "Klingon");
```

That is, the compiler can replace each instance of "Klingon" with the same address. If the compiler uses this single-copy representation and allows changing p1[0] to 'F', that would

```
printf("\nsizeof mytalents: %zd, sizeof yourtalents: %zd\n", sizeof(mytalents), sizeof(yourtalents));

return 0;
}
```

Here is the output:

Let's compare talents.
My Talents                        Your Talents
Adding numbers swiftly            Walking in a straight line
Multiplying accurately            Sleeping
Stashing data                     Watching television
Following instructions to the letter  Mailing letters
Understanding the C language      Reading email

sizeof mytalents: 40, sizeof yourtalents: 200

In some ways, mytalents and yourtalents are much alike. Each represents five strings. When used with one index, as in mytalents[0] and yourtalents[0], the result is a single string. And, just as mytalents[1][2] is 'l', the third character of the second string represented by mytalents, yourtalents[1][2] is 'e', the third character of the second string represented by yourtalents. Both are initialized in the same fashion.

But there are differences, too. The mytalents array is an array of five pointers, taking up 40 bytes on our system. But yourtalents is an array of five arrays, each of 40 char values, occupying 200 bytes on our system. So mytalents is a different type from yourtalents, even though mytalents[0] and yourtalents[0] both are strings. The pointers in mytalents point to the locations of the string literals used for initialization, which are stored in static memory. The arrays in yourtalents, however, contain copies of the string literals, so each string is stored twice. Furthermore, the allocation of memory in the arrays is inefficient, for each element of yourtalents has to be the same size, and that size has to be at least large enough to hold the longest string.

One way of visualizing this difference is to think of yourtalents as a rectangular two-dimensional array, with each row being of the same length, 40 bytes, in this case. Next, think of mytalents as a ragged array, one in which the row length varies. Figure 11.2 shows the two kinds of arrays. (Actually, the strings pointed to by the mytalents array elements don't necessarily have to be stored consecutively in memory, but the figure does illustrate the difference in storage requirements.)
