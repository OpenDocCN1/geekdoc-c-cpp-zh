# **26.3.3.2 Resource management**

Consider this nonsense function:

```
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

+   - The file named **s** is not closed
- The memory allocated for **p** is leaked if **b<=0** or if the second **new** throws
- The memory for **q** is leaked if **0<b**

In addition, we should always consider the possibility that an attempt at opening a file might fail. To get this miserable result, we deliberately used a very old-fashioned programming style (**open()** is the standard C way of opening files). We could have made the job for testers more straightforward by writing

```
void do_resources2(int a, int b, const char* s)    // less messy function
{
ifstream is(s);                        // open file
vector<int>v1(a);                      // create vector (owning memory)
if (b<=0) throw Bad_arg();             // maybe throw an exception
vector<int> v2(b);                     // create another vector (owning memory)
}
```

Now every resource is owned by an object with a destructor that will release it. Considering how we could write a function more simply (more cleanly) is sometimes a good way to get ideas for testing. The “Resource Acquisition Is Initialization” (RAII) technique from §19.5.2 provides a general strategy for this kind of resource management problem.

Please note that resource management is not just checking that every piece of memory allocated is deleted. Sometimes we receive resources from elsewhere (e.g.,