You are not obliged to initialize a pointer when you define it, but it's reckless not to. Uninitialized pointers are more dangerous than ordinary variables that aren't initialized. Therefore:

> > **Tip** As a rule, you should always initialize a pointer when you define it. If you cannot give it its intended value yet, initialize the pointer to `nullptr`.

It's relatively common to use variable names beginning with p for pointers, although this convention has fallen out of favor lately. Those adhering to what is called Hungarian notation—a somewhat dated naming scheme for variables—argue that it makes it easier to see which variables in a program are pointers, which in turn can make the code easier to follow. We will occasionally use this notation in this book, especially in more artificial examples where we mix pointers with regular variables. But in general, to be honest, we don't believe that adding type-specific prefixes such as p to variable names adds much value at all. In real code, it is almost always clear from the context whether something is a pointer or not.

In the examples earlier, we wrote the pointer type with the asterisk next to the type name, but this isn't the only way to write it. You can position the asterisk adjacent to the variable name, like this:

```
```cpp
long *pnumber {};
```
```

This defines precisely the same variable as before. The compiler accepts either notation. The former is perhaps more common because it expresses the type, "pointer to long," more clearly.

However, there's potential for confusion if you mix definitions of ordinary variables and pointers in the same statement. Try to guess what this statement does:

```
```cpp
long* pnumber {}, number {};
```
```

This defines two variables: one called pnumber of type "pointer to long", which is initialized with nullptr, and one called number of type long—not pointer to long—which is initialized with 0L. The fact that number isn't simply a second variable of type long* no doubt surprises you. The fact that you're surprised is no surprise at all; the notation that juxtaposes the asterisk and the type name makes it less than clear what the type of the second variable will be to say the least. It's a little clearer already if you define the two variables in this form:

```
```cpp
long *pnumber {}, number {};
```
```

This is a bit less confusing because the asterisk is now more clearly associated with the variable pnumber. Still, the only good solution really is to avoid the problem in the first place. It's much better to always define pointers and ordinary variables in separate statements:

```
```cpp
long number {};        // Variable of type long
long* pnumber {};      // Variable of type 'pointer to long'
```
```

Now there's no possibility of confusion, and there's the added advantage that you can append comments to explain how the variables are used.
Note that if you did want number to be a second pointer, you could write the following:

```
```cpp
long *pnumber {}, *number {};  // Define two variables of type 'pointer to long'
```
```