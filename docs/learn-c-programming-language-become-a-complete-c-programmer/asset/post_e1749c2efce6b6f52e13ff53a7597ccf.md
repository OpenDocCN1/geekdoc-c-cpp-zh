
```cpp
while (*q!=0){
*p++ = *q++;
}
*p=0; // terminating zero
```

The value of **`*p++ = *q++`** is **`*q`**. We can therefore rewrite the example like this:

```cpp
while ((*p++ = *q++) != 0) { }
```

In this case, we don’t notice that **`*q`** is zero until we already have copied it into **`*p`** and incremented **`p`**. Consequently, we can eliminate the final assignment of the terminating zero. Finally, we can reduce the example further by observing that we don’t need the empty block and that the **`!=0`** is redundant because the result of an integral condition is always compared to zero anyway. Thus, we get the version we set out to discover:

```cpp
while (*p++ = *q++);
```

Is this version less readable than the previous versions? Not to an experienced C or C++ programmer. Is this version more efficient in time or space than the previous versions? Except for the first version that called **`strlen()`**, not really; the performance will be equivalent and often identical code will be generated.

The most efficient way of copying a zero-terminated character string is typically the standard Cstyle string copy function:

```cpp
char * strcpy(char*, const char*); // from <string.h>
```

For more general copying, the standard **`copy`** algorithm (§4.5, §32.5) can be used. Whenever possible, use standard-library facilities in preference to fiddling with pointers and bytes. Standardlibrary functions may be inlined (§12.1.3) or even implemented using specialized machine instructions. Therefore, you should measure carefully before believing that some piece of handcrafted code outperforms library functions. Even if it does, the advantage may not exist on some other hardware+compiler combination, and your alternative may give a maintainer a headache.

## 11.2 Free Store

A named object has its lifetime determined by its scope (§6.3.4). However, it is often useful to create an object that exists independently of the scope in which it was created. For example, it is common to create objects that can be used after returning from the function in which they were created. The operator **`new`** creates such objects, and the operator **`delete`** can be used to destroy them. Objects allocated by **`new`** are said to be “on the *free store*” (also, “on the *heap*” or “in *dynamic memory*”).

Consider how we might write a compiler in the style used for the desk calculator (§10.2). The syntax analysis functions might build a tree of the expressions for use by the code generator:

```cpp
struct Enode {
Token_value oper;
Enode* left;
Enode* right;
// ...
```
};
Enode* expr(bool get) {
Enode* left = term(get);
for (;;) {
switch (ts.current().kind) {
case Kind::plus:
case Kind::minus:
left = new Enode {ts.current().kind,left,term(true)};
break;
default:
return left; // returnnode
}
}
}
```

In cases Kind::plus and Kind::minus, a new Enode is created on the free store and initialized by the value {ts.current().kind,left,term(true)}. The resulting pointer is assigned to left and eventually returned from expr().

I used the {}-list notation for specifying arguments. Alternatively, I could have used the oldstyle ()-list notation to specify an initializer. However, trying the = notation for initializing an object created using new results in an error:

```
int * p = new int = 7; // error
```

If a type has a default constructor, we can leave out the initializer, but built-in types are by default uninitialized. For example:

```
auto pc = new complex<double>; auto pi = new int;
// the complex is initialized to {0,0} // the int is uninitialized
```

This can be confusing. To be sure to get default initialization, use {}. For example: auto pc = new complex<double>{}; // the complex is initialized to {0,0} auto pi = new int{}; // the int is initialized to 0

A code generator could use the Enodes created by expr() and delete them:

```
void generate(Enode * n)
{
switch (n->oper) {
case Kind::plus:
// use n
delete n; // delete an Enode from the free store
}
}
```

An object created by new exists until it is explicitly destroyed by delete. Then, the space it occupied can be reused by new. A C++ implementation does not guarantee the presence of a “garbage collector” that looks out for unreferenced objects and makes them available to new for reuse. Consequently, I will assume that objects created by new are manually freed using delete.

### Section 11.2 Free Store 279

The **delete** operator may be applied only to a pointer returned by **new** or to the **nullptr**. Applying **delete** to the **nullptr** has no effect.
If the deleted object is of a class with a destructor (§3.2.1.2, §17.2), that destructor is called by **delete** before the object’s memory is released for reuse.

### 11.2.1 Memory Management

The main problems with free store are:

- *Leaked objects*: People use **new** and then forget to **delete** the allocated object.
- *Premature deletion*: People **delete** an object that they have some other pointer to and later use that other pointer.
- *Double deletion*: An object is deleted twice, invoking its destructor (if any) twice.

Leaked objects are potentially a bad problem because they can cause a program to run out of space. Premature deletion is almost always a nasty problem because the pointer to the “deleted object” no longer points to a valid object (so reading it may give bad results) and may indeed point to memory that has been reused for another object (so writing to it may corrupt an unrelated object). Consider this example of very bad code:

```
int * p1 = new int{99};
int* p2 = p1;
delete p1;
p1 = nullptr;
char* p3 = new char{'x'}; *p2 = 999;
cout << *p3 << '\n';
```

// potential trouble
// now p2 doesn't point to a valid object
// gives a false sense of safety
// p3 may now point to the memory pointed to by p2 // this may cause trouble
// may not print x

Double deletion is a problem because resource managers typically cannot track what code owns a resource. Consider:

```
void sloppy() // very bad code
{
int* p = new int[1000]; // ... use *p ...
delete[] p;

// acquire memory
// release memory
// ... wait a while ...
delete[] p; }
// but sloppy() does not own *p
```

By the second **delete[]**, the memory pointed to by *p may have been reallocated for some

other use and the allocator may get corrupted. Replace int with string in that example, and we’ll see string’s destructor trying to read memory that has been reallocated and maybe overwritten by other code, and using what it read to try to delete memory. In general, a double deletion is undefined behavior and the results are unpredictable and usually disastrous.

The reason people make these mistakes is typically not maliciousness and often not even simple sloppiness; it is genuinely hard to consistently deallocate every allocated object in a large program (once and at exactly the right point in a computation). For starters, analysis of a localized part of a program will not detect these problems because an error usually involves several separate parts.

As alternatives to using “naked” new s and delete, I can recommend two general approaches to resource management that avoid such problems:

- [1] Don’t put objects on the free store if you don’t have to; prefer scoped variables.
- [2] When you construct an object on the free store, place its pointer into a manager object (sometimes called a handle) with a destructor that will destroy it. Examples are string, vector and all the other standard-library containers, unique_ptr (§5.2.1, §34.3.1), and shared_ptr (§5.2.1, §34.3.2). Wherever possible, have that manager object be a scoped variable. Many classical uses of free store can be eliminated by using move semantics (§3.3, §17.5.2) to return large objects represented as manager objects from functions. This rule [2] is often referred to as RAII (“Resource Acquisition Is Initialization”; §5.2, §13.3) and is the basic technique for avoiding resource leaks and making error handling using exceptions simple and safe.

The standard-library vector is an example of these techniques:

```
void f(const string& s)
{
vector<char> v;
for (auto c : s)
v.push_back(c);
// ...
}
```

The vector keeps its elements on the free store, but it handles all allocations and deallocations itself. In this example, push_back() does new s to acquire space for its elements and delete s to free space that it no longer needs. However, the users of vector need not know about those implementation details and will just rely on vector not leaking.

The Token_stream from the calculator example is an even simpler example (§10.2.2). There, a user can use new and hand the resulting pointer to a Token_stream to manage:

```
Token_stream ts{new istringstream{some_string}};
```

We do not need to use the free store just to get a large object out of a function. For example:

```
string reverse(const string& s)
{
string ss;
for (int i=s.size()-1; 0<=i; --i)
```
