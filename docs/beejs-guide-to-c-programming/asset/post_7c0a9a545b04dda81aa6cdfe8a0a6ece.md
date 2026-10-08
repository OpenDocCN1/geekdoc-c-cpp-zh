
# Chapter 5. Pointers—Cower In Fear!

Hey, so we have here a variable that is a pointer type, and it can point to other ints. That is, it can hold the address of other ints. We know it points to ints, since it's of type int* (read "int-pointer").

When we do an assignment to a pointer variable, the type of the right hand side of the assignment has to be the same type as the pointer variable. Fortunately for us, when we take the address of a variable, the resultant type is pointer to that variable, so assignments like the following are perfect:

```
int i;
int *p; // p is a pointer, but uninitialized and points to garbage

p = &i; // p is assigned the address of i-- now "points" to i
```

On the left of the assignment, we have a variable of type int pointer-to-int (*), and on the right side, we have expression of type pointer-to-int is an int (address-of int gives you a pointer to int). The address of a thing can be stored in a pointer to that.

Get it? It still might not make much sense since you haven't seen an actual use for the pointer variable, we're taking small steps here that no one gets lost. Now, let's introduce you to the address-operator. It's kind of what address-of would be like in Blizzard World.

## 5.3 Dereferencing

A pointer variable can be thought of *referring to another by pointing to it. It's rare you'll hear anyone in C land talking "referring" or "references", but I bring it up so that the name of this operator will make a little more sense.

When you point to a pointer (roughly "a reference to a variable"), you can use the original through the pointer by *dereferencing* the pointer. (You) can think of this as "de-pointing" the pointer, or ever say "de-pointing".

Back to our analogy, this is vaguely looking like a home address and then going to that house.

Now, what do I mean by "get access to the original variable?" Well, if you have a variable called i, and you have a pointer to i, you can use the dereferenced pointer p exactly as if it were the original variable!

You have enough knowledge to handle an example. The last thing you need to know is exactly this: what is the dereference operator? It's actually the indirection operator, because you're accessing values indirectly via the pointer. And it is the asterisk: *. Now, don't get confused with the asterisk used in the pointer declaration, earlier. They are the same character, but they have different meanings in different contexts.

Here's a full-blown example:

```c
#include <stdio.h>

int main(void) {
    int i;
    int *p; // this is NOT a dereference--this is a type "int*"

    p = &i; // p now points to i, p holds address of i

    i = 10; // i is now 10
    *p = 20; // the p points to (namely!) i is now 20!!
}
```

> That's not all! It's used in /* */ and multiplication and in function prototypes with length arrays! It's the same, but the context gives it different meaning.

```c
printf("i is %d\n", i);    // prints "20"
printf("i is %d\n", *p);      // "20!" dereference-p is the same as i!
```

Remember that p holds the address of i, as you can see where we did the assignment to p on line 8. The indirection operator tells the computer to use the object pointer points instead of using the pointer itself. In this way, we have turned *p into an address of sorts for i.

Great, but why? Do any know of this?

## 5.4 Passing Pointers as Arguments

Right now, you're thinking that you have an awful of knowledge about pointers, but absolutely zero application, right? What if we use *p if you could just say i instead?

My friend, the real power of pointers comes into play when you pass them to functions. Why is this a big deal? You might recall from before that you could pass all arguments to functions and then they'd be duly copied into parameters, and then you could manipulate local copies of those variables within the function.

What if wanted to bring back more than one single piece of data from the function? I mean, can you only return one, right? What if I answered that question with another question? ...Er, two questions?

What happens when you pass a pointer as an argument to a function? Does a copy of the pointer get put into its corresponding variable? Your best sweat peaks it. Remember earlier I rambled on how EVERY SINGLE ARGUMENT got into parameters and the function uses a copy of the argument? Well, the same is true. Here is the function you get the pointer.

But, and this is the clever part: we will set up the pointer in advance to that variable... and then the function can dereference its copy of the pointer to get back to the original variable! The function can't see the variable, but it can certainly dereference a pointer to that!

This is analogous to writing a home address on a piece of paper, and then copying that onto another piece of paper. You now have two pointers to that, but both are equal to getting at getting you to the house itself.

In the case of a function call, one of the copies is stored in a pointer variable in the calling scope, and the other is stored in a pointer variable that is the parameter of the function.

Example! Let's revisit our own increment() function, but this time let's make it that it actually increments the value in the caller.

```c
#include <stdio.h>

void increment(int *p) // note that it accepts a pointer to an int
{
    *p = *p + 1;      // add one to the p pointers to
}

int main(void)
{
    int i = 10;
    int *j = &i;      // note the address-of; turns it into a pointer to i

    printf("i is %d\n", i);      // prints "20"
    printf("i is also %d\n", j);  // prints "10"

    increment(j);
}
```

Ok! There are a couple things to see here... not the least of which is that the increment() function takes an int as argument. We pass it an int in the call by changing the int variable i to an int * using the address-of operator. Remember, a pointer holds an address, so we make pointers to variables by incrementing them through the address-of operator.

The increment() function gets a copy of the pointer. Both the original pointer j (in main()) and the copy of that pointer p (the parameter in increment()) point to the same address, namely the one holding the value i. (Again, like two pieces of paper with the same address written on them). Dereferencing either allows you to modify the original variable i! The function can modify a variable in another scope! Rock!

The above example is more concisely written in the call by using address-of in the argument list:

```c
printf("i is %d\n", *j);
```

Pointer enthusiasts will recall early on in the guide, we used a pointer to read from the keyboard, scanf(). and although you might not have recognized it at the time, we used the address-of to pass a pointer to a value to scanf(). We do this because scanf() reads from the keyboard (typically) and stores the result in a variable. The only way to pass a pointer to a value to scanf() is to use the address-of operator. This is because the variables are not pointers by themselves.

## 5.5 The Null Pointer

Any variable of any type can be set to a special value called NULL. This indicates that the pointer doesn't point to anything.

```c
int *p = NULL;
```

If you try to dereference a NULL pointer, your program will crash. This is because NULL is not a valid memory address. It's a good practice to initialize pointers to NULL if they are not immediately used.

## 5.6 A Note on Declaring Pointers

The syntax for declaring a pointer can get a little weird. Let's look at this example:

```c
int a;
int b;
```

We can condense that into a single line, right:

```c
int a, b; // Same thing
```

So a and b are both ints. No problem. But what about this?

```c
int a;
int *p;
```

Can we make that into one line? We can. But where does the * go?

The rule is that the * goes in front of any variable that is a pointer type. That is, the * is not part of the int in this example. it's a part of p.

With in mind, we can write:

```c
int a, *p; // Same thing
```

It's important to note that the following line does not declare two pointers:

```c
int *p, q; // p is a pointer to an int; q is just an int.
```

So a look at this and determine which variables are pointers and which are not:

```c
int *a, b, c, *d, e, *f, g, h, *i;
```

I'll drop the answer in a footnote.

## 5.7 sizeof and Pointers

Just a line of syntax that might be confusing and you might see it from time to time.

Recall that sizeof operates on the type of the expression.

```c
int *p;
```

```c
// Prints size of an 'int'
printf("%zu\n", sizeof(int));
```

```c
// p is type 'int', so prints size of 'int*'
printf("%zu\n", sizeof(p));
```

```c
// p is type 'int', so prints size of 'int'
printf("%zu\n", sizeof(p));
```
