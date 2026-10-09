
have additional controls via a JTAG probe. In this case sometimes it is a good idea to halt the program at a position of interest using an infinite loop:
while(1);

the rest of the program follows and the idea is that the JTAG is used as a hardware debugger to restart and trace the program. Of course, what happens is that the optimizing compiler removes all of the code following the while as it is clearly unreachable and hence clearly dead code.

Another example, is when an exception is an observable effect, but the dead code is still eliminated. For example:

```
int a; 
int b = 0; 
a/b;
```

should throw an exception, but on GCC in default optimization mode it doesn't. The code is clearly dead as the result of a/b is never used, but it does have a side effect in that division by zero should always throw an exception. If you change the final line to:

```
int c = a/b;
```

then the exception occurs even though c is never used! You could say such a stupid program doesn't deserve consideration, but if you were writing a test to see if an exception was thrown you might want to disagree. Even stupid programs sometimes have their uses. Interestingly, marking a and b as volatile changes things, but only in that a and b are not optimized away, only the operation of a/b is removed:

```
volatile int a; 
volatile int b = 0; 
a/b;
```

There are many other examples, but the point here isn't so much to complain about compilers and standards which go against what you might want to do, but to expose the fact that compiler optimization isn't a simple concept or process. In practice, there are generally well-known ways around these problems – either turning off the offending optimization or making sure that the code has observable effects. This is not to say that programmers don't waste a great deal of time because of unwanted optimizations – far more time than that due to compiler bugs and errors. For example if you haven't seen it before trying to work out why a timing no op loop appears to take no time at all can take a great deal of effort.

It is also important to realize that optimizing compilers are a good thing, despite the occasional clash with the programmer's intent. It is very rare that I have been able to improve on the assembly language produced by GCC and reading it is often an education in itself.

## Undefined Behavior

The current concern is undefined behavior, UB – what it is, what it means and how to avoid it. However, as we have just seen, before undefined behavior hit the C headlines, we had unobservable behavior to cope with. In many ways the two are very similar, but undefined behavior takes on a more aggressive role.

Undefined behavior is a term used to specify that a particular operation has no meaning or is unpredictable. The idea is that the language specification refuses to specify what is to happen, leaving it up to someone else to supply an interpretation. This seems innocent enough, but over time it has morphed into something of a monster.

There is a great deal of argument about when the notion of undefined behavior first arose and much of it is about the placement and interpretation of commas in standards. Standards are not always particularly clear. What is clear is that, initially at least, undefined behavior was used to simply mean that the standard did not cover the situation. In this sense, if you wrote code that included undefined behavior then your program was not covered by the standard.

Perhaps the high point of undefined behavior's travel from reasonable to unreasonable was the famous “nasal demons” post in 1992 on a fairly “serious” newsgroup, comp.std.c:

> “*Undefined behavior -- behavior, upon use of a nonportable or erroneous program construct, ... for which the standard imposes no requirements. Permissible undefined behavior ranges from ignoring the situation completely with unpredictable results, to having demons fly out of your nose.*”

If you think that this humorous comment is extreme, a few posts earlier we have:

> “*At this point, the compiler is at liberty to generate a program which formats your hard disk drive. In fact, it probably should.*”

The idea that if a program contained undefined behavior then all bets were off grew and continues to grow from this point. It is the programmer's equivalent of the principle of explosion. If you have two logical premises, P and !P, and you assume that they are both true, then anything can be proved true. The reasoning is:

P is true so P or Q is true no matter what Q is. But as !P is true P or Q implies that Q is true. Hence any statement can be proved true if P and !P are assumed.

So rejecting the law that only one of P or !P can be true, leads to a situation in which logical demons can fly out of your nose.

Of course, in practice, the existence of the principle of explosion is an argument for anything that invokes it is meaningless. So too with undefined behavior – its exploitation produces meaningless program semantics. And yet we still have the confusing idea that undefined behavior is at the same time somehow useful, and yet something that programmers need to identify and eliminate if they want to avoid nasal demons. It also gives you some idea of how out of touch compiler writers can be when they don't appreciate the uses of the language they are trying to compile.

There is a huge difference between stating that the standard does not define what happens in a particular case and thinking that this gives you carte blanche to do whatever you want. It seems that what happened was that the standards committee discovered it was easier to leave some behavior to the machine the program was running on to deal with, but instead of marking it as machine-dependent or implementation-dependent they chose to represent it as simply being outside of the standard and then the rest followed.

### UB in Practice

The reputation of undefined behavior, UB, has caused many programmers to focus on it and avoid anything that has been defined as such. This is an overreaction because many undefined behaviors are perfectly well-defined in practice and, in many cases, desirable rather than avoidable. The important thing to realize is that despite being threatened with nasal demons and reformatting of disks, this rarely happens.

In practice undefined behavior is mostly a nuisance just like the optimizations that don't take account of what might be observable. Indeed one of the examples given of dead code deletion could just as well be listed as undefined behavior as dividing by zero is listed as such. So when you write:

```
int a;
int b = 0;
int c = a/b;
```

you have already got undefined behavior, even if you then don't make use of c and have deadcode. In practice, what happens is not nasal demons but something much worse – an exception.

Of course, division by zero is something you need to protect against – even if it wasn't undefined behavior. The usual way to do this is to use an if statement:

```
if (b!=0) c = a/b;
```

or make use of lazy evaluation:

```
c = b & a/b;
```

Most other undefined behaviors are treated in a similar way and as long as you write a good program that protects itself against the obvious, nasal demons will ignore you. For example, undefined behavior that falls into this category includes:

- Accessing array outside of bounds
- Modifying a string literal
- Dereferencing/accessing a null pointer
- Changing a variable twice between sequence points
- Shifting by negative amounts
- Accessing uninitialized data

These and many others are very reasonable and easy-to-deal with, but some are more problematic, signed overflow and strict aliasing being the most important.

### Divide By Zero and Undefined Behavior

It is worth explaining the crazy position of divide by zero in C99:

> C99 6.5.5p5 - The result of the / operator is the quotient from the division of the first operand by the second; the result of the % operator is the remainder. In both operations, if the value of the second operand is zero, the behavior is undefined.

If you need a clear demonstration that undefined behavior is completely mad and unacceptable, this is it.

You will find some programmers arguing that x/0 is infinity because x/y with x and y positive gets bigger as y trends to 0. This is true, but mathematicians define x/y as undefined if y equals 0. The reason is that the operation makes no logical sense. For example: x.0 = 0 doesn't have a unique solution and 0 is the only number that doesn't have a multiplicative inverse.

So it looks as if deciding that division by zero is undefined is justified – but that would be wrong. The idea that encountering y/0 is a permission to do anything the compiler writer can think of is nonsense. A program that includes y/0 may be an incorrect program, but the correct behavior is to indicate that the operation is illegal. The program has to report the error or throw an exception or at the most general perform some action which is machine dependent.

Division by zero is a runtime error not undefined behavior.
