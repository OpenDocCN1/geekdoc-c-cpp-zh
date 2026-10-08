# Chapter 15. Types III: Conversions

If you want to know the gritty details, check out C11 §6.3.1.8. But you probably don't.

Just remember that int types become float if there's a floating point type anywhere in there, and the compiler makes an effort to make mixed integer types don't overflow.

Finally, if you convert from one floating point type to another, the compiler will try to make an exact conversion. If it can't, it'll do the best approximation it can. If the number is too large to fit in the type you're converting into, boom: undefined behavior!

# 15.4.3 void*

The void* is interesting because it can be converted from or any pointer type.

```
int x = 10;
```

```
void *p = &x;      // x is type int, but we store it in a void*
int *q = p;       // p is void*, but we store it in an int *
```

# 15.5 Explicit Conversions

These are conversions from type to type that you have to ask for; the compiler won't do it for you.
You can convert from one type to another by assigning one type to another with an =
You can also convert explicitly with a _cast.

# 15.5.1 Casting

You can easily change the type of an expression by putting a new type in parentheses in front of it. Some C frown on the practice unless absolutely necessary, it's likely you'll come across some C code with these in it.

Let's an example where we want to convert an int into a long so that we can store it in a long.

Note: this example is contrived and the cast in this case is completely unnecessary because the x + 12 expression would be automatically changed to long to match the wider of y.

```
int x = 10;
long y = (long)x + 12;
```

More commonly, you might see a cast being used to convert a void* to a specific pointer type so it can be dereferenced.

A callback from the builtin-qsort function may display this behavior since it has void* passed into it:

```
int compare(const void *elem1, const void *elem2)
{
    if ((*const int*)elem2) > ((*const int*)elem1)) return 1;
    if ((*const int*)elem2) < ((*const int*)elem1)) return -1;
    return 0;
}
```

But you could clearly write it with an assignment:

```
int compare(const void *elem1, const void *elem2)
{
```