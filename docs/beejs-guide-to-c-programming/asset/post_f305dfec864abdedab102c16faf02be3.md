
## Chapter 20. structs II: More Fun with structs

Since the members of a union share the same memory, writing to one member necessarily affects the others. And if you read from one what was written to another, you will get some weird effects.

```c
#include <stdio.h>
```

```c
union foo {
  float b;
  short a;
};

int main(void) {
  union foo x;

  x.b = 3.14159;

  printf("%f\n", x.b); // 3.14159, fair enough

  printf("%d\n", x.a); // But what about this?
}
```

On my system, this prints out:
3.141590
4048

because under the hood, the object representation for the float 3.14159 was the same as the object representation for the short 4048. On my system. Your results may vary.

## 20.9.2 Pointers to unions

If you have a pointer to a union, you can cast pointer to any of the types of the fields in that union and get the values out that way.

In this example, we see that the union has ints and floats in it. And we get pointers to the union, way we cast them to *int* and *float* types (the cast silences compiler warnings). And then if we dereference those, we will see that the values were stored directly in the union.

```c
#include <stdio.h>
```

```c
union foo {
  int a, b, c, d, e, f;
  float g, h;
  char i, j, k, l;
};

int main(void) {
  union foo x;

  int *foo_int_p = (int *)&x;
  float *foo_float_p = (float *)&x;

  x.a = 12;
  printf("%d\n", x.a);      // 12
  printf("%d\n", *foo_int_p); // 12, again
}
```

The reverse is also true. If we have a pointer to type inside the union, we can cast that to a pointer to the union and access its members.

```c
union foo x;
int *foo_int_p = (int *)&x;      // Pointer to int field
union foo *p = (union foo *)foo_int_p;  // Back to pointer to union

p->a = 12;                      // This line the same as...
x.a = 12;                        // this one.
```

All this tells us that, under the hood, all these values in a union start at the same place in memory, and that's the same as where the entire union is.

## 20.9.3 Common Initial Sequences in Unions

If you have a union of structs, and all those structs begin with a common initial sequence, it's valid to access members of that sequence from any of the union members.

What? Here are two structs with a common initial sequence:

```c
struct a {
  int x;           //
  float y;         // Common initial sequence
};

struct b {
  int x;           //
  float y;         // Common initial sequence

  double *p;
  short z;
};
```

Do you see it? It's they start with int followed by float—that's the common initial sequence. The members in the sequence of the structs have to be compatible types. And we see that with x and y, which are int and float relatively.

Now let's build a union of these:

```c
union foo {
  struct a sa;
  struct b sb;
};
```

This rule tells us that we are guaranteed that the members of the common initial sequences are interchangeable in code. That is:

- f.sa.x is as same as f.sb.x.

and

- f.sa.y is the same as f.sb.y.

Because fields x and y are both in the common initial sequence.

Also, the names of the members in the common initial sequence don't matter—all that matters is that the types are the same.

All together, this allows us to safely add some shared information between structs in the union. The best example of this is probably using a field to determine the type of struct out of the structs in the union that is "in use".

That is, if we weren't allowed this and passed the union to some function, how would that function know which member of the union was the one it should look at?

Take a look at these structs. Note the common initial sequence:

```c
#include <stdio.h>

struct common {
    int type; // common initial sequence
};

struct antelope {
    int type; // common initial sequence
    int loudness;
};

struct octopus {
    int type; // common initial sequence

    int sea_creature;
    float intelligence;
};
```

Now let's throw them into a union:

```c
union animal {
    struct common common;
    struct antelope antelope;
    struct octopus octopus;
}
```

Also, please indulge these two #defines for the demo:

```c
#define ANTELOPE 1
#define OCTOPUS 2
```

So far, nothing special has happened here. It seems the type field is completely useless. But now let's make a generic function that prints union. It has to somehow be able to tell if it's looking at struct antelope or a struct octopus. Because of the magic of initial sequences, it can look up the type in any of these places for a particular union:

```c
int type = x.common.type; // or...
int type = x.antelope.type; // or...
int type = x.octopus.type; // or...
```

All refer to the same value in memory.

```c
void print_animal(union animal *x) {
    switch (x->common.type) {
        case ANTELOPE:
            printf("Antelope loudness=%d\n", x->loudness);
            break;
        case OCTOPUS:
            printf("Octopus sea_creature=%d\n", x->sea_creature);
            printf("intelligence=%f\n", x->intelligence);
            break;
        default:
            printf("Unknown type %s\n");
    }
}
```

```c
int main(void) {
    union animal a = {.type=ANTELOPE, .loudness=12};
    union animal b = {.type=OCTOPUS, .sea_creature=1, .intelligence=12};

    print_animal(&a);
    print_animal(&b);
}
```

See how on line 29 we're just passing in the union—we have no idea what type of struct is use within it. But that's OK! Because on line 31 we check the type to see if it's an antelope or an octopus, and then we can look up the members to get the memory-saving effects of union.

## 20.10 Unions and Unnamed Structs

You know you can have an unnamed struct, like this:

```c
struct {
    int x, y;
} s;
```

That defines a variable s that is of anonymous type (because the struct has no name), members x and y. So things like this are valid:

```c
s.x = 34;
s.y = 90;
printf("%d %d\n", s.x, s.y);
```

Turns out you can drop those unnamed structs in unions like you might expect:

```c
union foo {
  struct {
    // unnamed!
    int x, y;
  } a;

  struct {
    // unnamed!
    int z, w;
  } b;
};
```

And then access them as per normal:

```c
union foo f;
f.a.x = 1;
f.a.y = 2;
f.b.z = 3;
f.b.w = 4;
```

No problem!

## 20.11 Passing and Returning structs and unions

You can pass a struct or union to a function by value (as opposed to a pointer to it)—a copy of object to the parameter will be as if assignment per usual. You can also return a struct or union from a function and it is also passed by value back.

```c
#include <stdio.h>
```

```c
struct foo {
    int x, y;
};
```

```c
struct foo f(void) {
    return (struct foo){.x=34, .y=90};
}
```

```c
int main(void) {
    struct foo a = f(); // Copy is made
    printf("%d %d\n", a.x, a.y);
}
```

Fun fact: if you do this, you can use the . operator right off the function call:

```c
printf("%d %d\n", f().x, f().y);
```

(Of course example calls the function twice, efficiently.)

And the same holds true for returning pointers to structs and unions—just be sure to use the -> operator in that case.

## Chapter 21

## Characters and Strings II

We've talked about how char types are actually just integer types... but it's the same for a character in single quotes. But a string in double quotes is type const char *.

Turns out there are few more of strings and characters, and it leads down one of the most infamous rabbit holes in the language: the whole multibyte/wide/Unicode/localization thing. We're going to peer into that rabbit hole, but not go in. ...Yet!

## 21.1 Escape Sequences

We're used to strings and characters with regular letters, punctuation, and numbers: but if we want some special characters in there that we can't type on the keyboard because they don't exist (e.g. "\"):

```c
char t = '\\';
```

To do these, we use something called escape sequences. These are the backslash character (\) followed by another character. The two (or more) characters together have special meaning.

For our single quote character example, we can put an escape (that is, \) in front of the central single quote to solve it:

Now C knows that \ means just a regular character we want to print, not the end of the sequence.

## 21.1.1 Frequently-used escapes

In my humble opinion, these escape characters make up 99.2%¹ of all escapes.
