Like a (data) object, the code generated for a function body is placed in memory somewhere, so it has an address. We can have a pointer to a function just as we can have a pointer to an object. However, for a variety of reasons – some related to machine architecture and others to system design – a pointer to function does not allow the code to be modified. There are only two things one can do to a function: call it and take its address. The pointer obtained by taking the address of a function can then be used to call the function. For example:

```
void error(string s) {/*...*/}
pointer to function taking a string argument and returning nothing void (*efct)(string); //
void f() {
efct = &error; // efct points to error
efct("error"); // call error through efct
}
```

The compiler will discover that efct is a pointer and call the function pointed to. That is, dereferencing a pointer to function using * is optional. Similarly, using & to get the address of a function is optional:

```
void (*f1)(string) = &error; void (*f2)(string) = error;
// OK: same as = error // OK: same as = &error
void g() { f1("Vasa"); // OK: same as (*f1)("Vasa")
(*f1)("Mary Rose"); // OK: as f1("MaryRose")
}
```

Pointers to functions have argument types declared just like the functions themselves. In pointer assignments, the complete function type must match exactly. For example:

```
void (*pf)(string); // pointer to void(str ing)
void f1(string); // void(str ing)
int f2(string); // int(string)
void f3(int*); // void(int*)
void f() {

pf = &f1; // OK
pf = &f2; // error : bad return type pf = &f3; // error :bad argument type

pf("Hera"); // OK
pf(1); // error :bad argument type
int i = pf("Zeus"); // error :void assigned to int
}
```

The rules for argument passing are the same for calls directly to a function and for calls to a function through a pointer.
You can convert a pointer to function to a different pointer-to-function type, but you must cast the resulting pointer back to its original type or strange things may happen:

```
using P1 = int(*)(int*);
using P2 = void(*)(void);
```