
## 26.3.3.1 Dependencies

By “explicit or implicit” we mean that we have to look not just at the formal parameters and the return value, but also at any effects on global variables, **io-streams**, files, free-store memory allocation, etc. So, what can we do? First of all, such a function is almost certainly too long – or we could have stated its requirements and effects more clearly. Maybe we are talking about a function that is five pages long or uses “helper functions” in complicated and non-obvious ways. You may think that five pages is a lot for a function. It is, but we have seen much, much longer functions than that. Unfortunately, they are not uncommon.

If it is our code and if we had time, we would first of all try to break such a “messy function” up into smaller functions that come closer to our ideals of a well-specified function and first test those. However, here we will assume that our aim is to test the software – that is, to systematically find as many errors as possible – rather than (just) fixing bugs as we find them.

So, what do we look for? Our job as testers is to find errors. Where are bugs likely to hide? What characterizes code that is likely to contain bugs?

- Subtle dependencies on “other code”: look for use of global variables, non-**const**-reference arguments, pointers, etc.
- Resource management: look for memory management (**new** and **delete**), file use, locks, etc.
- Look for loops: check end conditions (as for `binary_search()`).
- **if**-statements and switches (often referred to as “branching”): look for errors in their logic.

Let's look at examples of each.

### 26.3.3.1 Dependencies

Consider this nonsense function:

```cpp
int do_dependent(int a, int& b)          // messy function
{
     // undisciplined dependencies
     int val ;
     cin>>val;
     vec[val] += 10;
     cout << a;
     b++;
     return b;
}
```

To test `do_dependent()`, we can't just synthesize sets of arguments and see what it does with them. We have to take into account that it uses the global variables `cin`, `cout`, and `vec`. That's pretty obvious in this little nonsense function, but in real code this may be hidden in a larger amount of code. Fortunately, there is software that can help us find such dependencies. Unfortunately, it is not always easily available or widely used. Assuming that we don't have analysis software to help us, we go through the function line by line, listing all its dependencies.

To test `do_dependent()`, we have to consider:

- Its inputs:
    - The value of **a**
    - The value of **b** and the value of the int referenced by **b**
    - The input from `cin` (into `val`) and the state of `cin`
    - The state of `cout`
    - The value of `vec`, in particular, the value of `vec[val]`
- Its outputs:
    - The return value
    - The value of the int referenced by **b** (we incremented it)
    - The state of `cin` (beware of stream state and format state)
    - The state of `cout` (beware of stream state and format state)
    - The state of **vec** (we assigned to **vec[val]**)
    - Any exceptions that `vec` might have thrown (`vec[val]` might be out of range)

This is a long list. In fact, that list is longer than the function itself. This goes a long way toward explaining our dislike of global variables and our concerns about non-const references (and pointers). There really is something very nice about a function that just reads its arguments and produces a result as a return value: we can easily understand and test it.

Once the inputs and outputs are identified, we are basically back to the `binary_search()` case. We simply generate tests with input values (for explicit and implicit inputs) to see if they give the desired outputs (considering both implicit and explicit outputs). With `do_dependent()`, we would probably start with a very large `val` and a negative `val`, to see what happens. It looks as if `vec` had better be a range-checked vector (or we can very simply generate really bad errors). We would of course check what the documentation said about all those inputs and outputs, but with a messy function like that we have little hope of the specification being complete and precise, so we will just break the functions (i.e., find errors) and start asking questions about what is correct. Often, such testing and questions should lead to a redesign.

### 26.3.3.2 Resource management

Consider this nonsense function:

```cpp
void do_resources1(int a, int b, const char* s)    // messy function
// undisciplined resource use
{
FILE* f = fopen(s,"r");            // open file (C style)
int* p = new int[a];               // allocate some memory
if (b<=0) throw Bad_arg();        // maybe throw an exception
int* q = new int[b];              // allocate some more memory
delete[] p;                        // deallocate the memory pointed to by p
}
```

To test **do_resources1()**, we have to consider whether every resource acquired has been properly disposed of, that is, whether every resource has been either released or passed to some other function.

Here, it is obvious that

- The file named **s** is not closed
- The memory allocated for **p** is leaked if **b<=0** or if the second **new** throws
- The memory for **q** is leaked if **0<b**

In addition, we should always consider the possibility that an attempt at opening a file might fail. To get this miserable result, we deliberately used a very old-fashioned programming style (**fopen()** is the standard C way of opening files). We could have made the job for testers more straightforward by writing

```cpp
void do_resources2(int a, int b, const char* s)    // less messy function
{
ifstream is(s);                        // open file
vector<int>v1(a);                      // create vector (owning memory)
if (b<=0) throw Bad_arg();             // maybe throw an exception
vector<int> v2(b);                     // create another vector (owning memory)
}
```

Now every resource is owned by an object with a destructor that will release it. Considering how we could write a function more simply (more cleanly) is sometimes a good way to get ideas for testing. The “Resource Acquisition Is Initialization” (RAII) technique from §19.5.2 provides a general strategy for this kind of resource management problem.

Please note that resource management is not just checking that every piece of memory allocated is deleted. Sometimes we receive resources from elsewhere (e.g., as an argument), and sometimes we pass resources out of a function (e.g., as a return value). It can be quite hard to determine what is right about such cases. Consider:

```cpp
FILE* do_resources3(int a, int* p, const char* s)
// messy function
// undisciplined resource passing
{
FILE* f = fopen(s,"r");
delete p;
delete var;
var = new int[27];
return f;
}
```

Is it right for `do_resources3()` to pass the (supposedly) opened file back as the return value? Is it right for `do_resources3()` to delete the memory passed to it as the argument `p`? We also added a really sneaky use of the global variable `var` (obviously a pointer). Basically, passing resources in and out of functions is common and useful, but to know if it is correct requires knowledge of a resource management strategy. Who owns the resource? Who is supposed to delete/release it? The documentation should clearly and simply answer those questions. (Dream on.) In either case, passing of resources is a fertile area for bugs and a tempting target for testing.

Note how we (deliberately) complicated the resource management example by using a global variable. Things can get really messy when we start to mix the sources of likely bugs. As programmers, we try to avoid that. As testers, we look for such examples as easy pickings.

### 26.3.3.3 Loops

We have looked at loops when we discussed `binary_search()`. Basically most errors occur at the ends:

- Is everything properly initialized when we start the loop?
- Do we correctly end with the last case (often the last element)?

Here is an example where we get it wrong:

```cpp
int do_loop(const vector<int>& v)
// messy function
// undisciplined loop
{
int i;
int sum;
while (i<=vec.size()) sum+=v[i];
return sum;
}
```
