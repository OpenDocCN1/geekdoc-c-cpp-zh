Of course, in practice, the existence of the principle of explosion is an argument for anything that invokes it is meaningless. So too with undefined behavior – its exploitation produces meaningless program semantics. And yet we still have the confusing idea that undefined behavior is at the same time somehow useful, and yet something that programmers need to identify and eliminate if they want to avoid nasal demons. It also gives you some idea of how out of touch compiler writers can be when they don't appreciate the uses of the language they are trying to compile.

There is a huge difference between stating that the standard does not define what happens in a particular case and thinking that this gives you carte blanche to do whatever you want. It seems that what happened was that the standards committee discovered it was easier to leave some behavior to the machine the program was running on to deal with, but instead of marking it as machine-dependent or implementation-dependent they chose to represent it as simply being outside of the standard and then the rest followed.

# UB in Practice

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