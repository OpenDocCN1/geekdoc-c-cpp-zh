```
```c
21
22 static A a ;
23 int main ( )
24 {
25 }
26
```
```

# ### Solution of Question 42

Output of the program is:

```
```
f2()
f1()
```
```

It is self-explanatory.

# ### ** Question 43 Storage Duration

How many types of storage duration is possible with a given object once it is created ?

# ### Solution of Question 43

There are four types of storage duration determining the minimum potential lifetime of the storage containing the object as given below:

+   1. dynamic storage duration : enabled by the global allocation functions *operator new* and *operator new[]*,
+   2. static storage duration : enabled by *static*. The storage for these entities shall last for the duration of the program.
+   3. thread storage duration : enabled by *thread_local*
+   4. automatic storage duration : enabled by *register* or not explicitly declared *static* or *extern*.

# ### * Question 44 Integral Types

What are integral types ?

# ### Solution of Question 44

The following types are collectively called *Integral Types*:

+   * bool
+   * char
+   * char16_t
+   * char32_t