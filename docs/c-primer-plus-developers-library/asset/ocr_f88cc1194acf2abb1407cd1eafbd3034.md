Objects of such classes can be invoked by using function notation but can carry additional information. Adaptable functors, for example, have typedef statements that identify the argument types and the return value type for the functor. This information can be used by other components, such as function adapters.

By representing common container types and providing a variety of common operations implemented with efficient algorithms, all done in a generic manner, the STL provides an excellent source of reusable code. You may be able to solve a programming problem directly with the STL tools, or you may be able to use them as building blocks to construct the solution you need.

The complex and valarray template classes support numeric operations for complex numbers and arrays.

# Chapter Review

+   1. Consider the following class declaration:

```
class RQ1
{
private:
    char * st;        // points to C-style string
public:
    RQ1() { st = new char [1]; strcpy(st,""); }
    RQ1(const char * s)
    { st = new char [strlen(s) + 1]; strcpy(st, s); }
    RQ1(const RQ1 & rq)
    { st = new char [strlen(rq.st) + 1]; strcpy(st, rq.st); }
    ~RQ1() { delete [] st; }
    RQ1 & operator=(const RQ1 & rq);
    // more stuff
};
```

Convert this to a declaration that uses a string object instead. What methods no longer need explicit definitions?

+   2. Name at least two advantages string objects have over C-style strings in terms of ease-of-use.

+   3. Write a function that takes a reference to a string object as an argument and that converts the string object to all uppercase.

+   4. Which of the following are not examples of correct usage (conceptually or syntactically) of auto_ptr? (Assume that the needed header files have been included.)

```
auto_ptr<int> pia(new int[20]);
auto_ptr<string> pis(new string);
int * prique = 7;
auto_ptr<int> pr(&prique);
auto_ptr dbl (new double);
```