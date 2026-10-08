point p = {.x=20, .y=40};

printf("%d, %d\n", p.x, p.y); // 20, 40

# 10.2.2 typedef and Other Types

It's not using typedef with a simple type like int is completely useless... it helps you abstract the types to make it easier to change them later.

For example, if you float all over your code in 100 zillion places, it's going to be painful to change all to double if you find you have to do that later for some reason.

But if you prepared a little with:

```
typedef float app_float;

//
app_float f1, f2, f3;
```

Then if you want to change to another type, long long double, you just need to change the typedef:

```
//  voila!
//  |------|
typef double app_float;
```

// and no need to change this line:

```
app_float f1, f2, f3; // Now these are all long declaration.
```

# 10.2.3 typedef and Pointers

You can make a type that is a pointer.

```
typedef int *intptr;
```

```
int a = 10;
intptr x = &a; // "intptr" is type "int*"
```

I really don't like this practice. It hides the fact that x is a pointer type because you don't see a * in the declaration.

IMHO, it's better to explicitly show that you're declaring a pointer type so that others devs clearly see it and not mistake x for having a non-pointer type.

But at last count, say, 832,007 people had a different opinion.

# 10.2.4 typedef and Capitalization

I've seen all kinds of capitalization on typedef.

```
typedef struct {
int x, y;
} my_point; // lower snake case
```

```
typedef struct {
int x, y;
} MyPoint; // CamelCase
```