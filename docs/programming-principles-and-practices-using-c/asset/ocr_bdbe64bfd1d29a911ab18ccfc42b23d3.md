probably OK for such a trivial computation). However, we could be a bit more explicit:

```
```
int area(int length, int width)
// calculate area of a rectangle;
// pre-conditions: length and width are positive
// post-condition: returns a positive value that is the area
{
    if (length<=0 || width <=0) error("area() pre-condition");
    int a =  length*width;
    if (a<=0) error("area() post-condition");
    return a;
}
```
```

We couldn't check the complete post-condition, but we checked the part that said that it should be positive.

# **TRY THIS**

Find a pair of values so that the pre-condition of this version of area holds, but the post-condition doesn't.

Pre- and post-conditions provide basic sanity checks in code. As such they are closely connected to the notion of invariants (\$9.4.3), correctness (\$4.2, \$5.2), and testing (Chapter 26).

# ### 5.11 Testing

How do we know when to stop debugging? Well, we keep debugging until we have found all the bugs – or at least we try to. How do we know that we have found the last bug? We don't. "The last bug" is a programmers' joke: there is no such creature; we never find "the last bug" in a large program. By the time we might have, we are busy modifying the program for some new use.

In addition to debugging we need a systematic way to search for errors. This is called *testing* and we'll get back to that in \$7.3, the exercises in Chapter 10, and in Chapter 26. Basically, testing is executing a program with a large and systematically selected set of inputs and comparing the results to what was expected. A run with a given set of inputs is called a *test case*. Realistic programs can require millions of test cases. Basically, systematic testing cannot be done by humans typing in one test after another, so we'll have to wait a few chapters before we