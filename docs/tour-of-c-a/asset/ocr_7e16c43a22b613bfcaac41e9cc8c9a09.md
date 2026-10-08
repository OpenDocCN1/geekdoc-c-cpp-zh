```
void rotate_and_draw(vector<S>& v, int r)
{
    for_each(v,[](auto& s){ s->rotate(r); s->draw(); });
}
```

Here, in variable declarations, auto means that a value of any type is accepted as an initializer (an argument is considered to initialize the parameter). This makes a lambda with auto parameter template, a generic lambda. When needed, we can constrain the parameter with a concept (§8.2). For example, we could define Pointer_to_class rotate * and ->

and write:

Click here to view code image

```
for_each(v,[](Pointer_to_class auto& s){ s->rotate(r); s->draw(); });
```

We can call this generic rotate_and_draw with any container of objects that you can draw and rotate().

Click here to view code image

```
void user()
{
    vector<unique_ptr<Shape>> v1;
    vector<Shape> v2;
    //
    rotate_and_draw(v1,45);
    rotate_and_draw(v2,90);
}
```

For even tighter checking, we define a Pointer_to_Shape concept specifying the properties we want for a type to be usable as a shape. That would allow us to use shapes that aren't derived from class Shape.

# 7.3.3.2 Lambdas for initialization

Using a lambda, we can turn any statement into an expression. This is mostly useful to provide an operation to compute as an argument value, but the ability is general. Consider a complicated initialization:

Click here to view code image

```
enum init_mode { zero, scpy, patn }; // initializer alternatives
void user(init_mode m, int n, vector<int>& arg, Iterator p, Iterator q)
{
    vector<int> v;
    // messy initialization code:
    switch (m) {
        case zero:
            v = vector<int>(n); // n elements initialized to 0
            break;
        case scpy:
            v = arg;
            break;
}
```