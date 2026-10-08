```
```text
struct Shape1 {
    enum Kind { circle, rectangle } kind;
    /* ... */
};

void draw(struct Shape1* p)
{
    switch (p->kind) {
    case circle:
        /* draw as circle */
        break;
    case rectangle:
        /* draw as rectangle */
        break;
    }
}

int f(struct Shape1* pp)
{
    draw(pp);
    /* ... */
}
```
```

This works. There are two snags, though:

+   - For each “pseudo-virtual” function (such as **draw()**), we have to write a new **switch**-statement.
- Each time we add a new shape, we have to modify every “pseudo-virtual” function (such as **draw()**) by adding a case to the **switch**-statement.

The second problem is quite nasty because it means that we can’t provide our “pseudo-virtual” functions as part of a library, because our users will have to modify those functions quite often. The most effective alternative involves pointers to functions:

```
```text
typedef void (*Pctf0)(struct Shape2*);
typedef void (*Pctfint)(struct Shape2*,int);

struct Shape2 {
    Pctf0 draw;
    Pctfint rotate;
    /* ... */
};
```
```