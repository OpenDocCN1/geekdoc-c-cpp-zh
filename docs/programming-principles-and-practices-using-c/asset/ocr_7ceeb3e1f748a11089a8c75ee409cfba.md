quires. If you can't state that simply and precisely in a couple of comment lines, you probably haven't thought hard enough about what you are doing. Experience shows that writing those pre-condition comments and the pre-condition tests helps you avoid many design mistakes. We did mention that we hated debugging; explicitly stating pre-conditions helps in avoiding design errors as well as catching usage errors early. Writing

```
```
int my_complicated_function(int a, int b, int c)
// the arguments are positive and a < b < c
{
if (!(0<a && a<b && b<c))       // ! means "not" and && means "and"
error("bad arguments for mcf");
// ...
}
```
```

saves you time and grief compared with the apparently simpler

```
```
int my_complicated_d_function(int a, int b, int c)
{
// ...
}
```
```

# ## 5.10.1 Post-conditions

Stating pre-conditions helps us improve our design and catch usage errors early. Can this idea of explicitly stating requirements be used elsewhere? Yes, one more place immediately springs to mind: the return value! After all, we typically have to state what a function returns; that is, if we return a value from a function we are *always* making a promise about the return value (how else would a caller know what to expect?). Let's look at our area function (from \S 5.6.1) again:

```
```
// calculate area of a rectangle;
// throw a Bad_area exception in case of a bad argument
int area(int length, int width)
{
if (length<=0 || width<=0) throw Bad_area();
return length*width;
}
```
```

It checks its pre-condition, but it doesn't state it in the comment (that may be OK for such a short function) and it assumes that the computation is correct (that's