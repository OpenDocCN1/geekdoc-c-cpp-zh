Note the duality of allocation and release: the single-object allocation requires a single-object release and the array allocation demands an array release. Otherwise the run-time system will handle the deallocation incorrectly and most likely crash at this point. Pointers can also refer to other variables:

```
```
int i = 3;
int* ip2 = &i;
```
```

The operator & takes an object and returns its address. The opposite operator is * which takes an address and returns an object:

```
```
int j = *ip2;
```
```

This is called Dereferencing. Given the operator priorities and the grammar rules, the meaning of the symbol * as dereference or multiplication cannot be confused—at least not by the compiler.

Pointers that are not initialized contain a random value (whatever bits are set in the corresponding memory). Using uninitialized pointers can cause any kind of error. To say explicitly that a pointer is not pointing to something, we should set it to

```
```
int* ip3 = nullptr; // >= C++11
int* ip4{}; // ditto
```
```

or in old compilers:

```
```
int* ip3 = 0; // better not in C++11 and later
int* ip4 = NULL; // ditto
```
```

The address 0 is guaranteed never to be used for applications, so it is safe to indicate this way that the pointer is empty (not referring to something). Nonetheless the literal 0 does not clearly convey its intention and can cause ambiguities in function overloading. The macro NULL is not better: it just evaluates to 0. C++11 introduces nullptr as a keyword for a pointer literal. It can be assigned to or compared with all pointer types. As it cannot be confused with other types and is self-explanatory, it is preferred over the other notations. The initialization with an empty braced list also sets a nullptr.

The biggest danger of pointers is Memory Leaks. For instance, our array y became too small and we want to assign a new array:

```
```
int* y = new int[15];
```
```

We can now use more space in y. Nice. But what happened to the memory that we allocated before? It is still there but we have no access to it anymore. We cannot even release it because this requires the address too. This memory is lost for the rest of our program execution. Only when the program is finished will the operating system be able to free it. In our example, we only lost 40 bytes out of several gigabytes that we might have. But if this happens in an iterative process, the unused memory grows continuously until at some point the whole (virtual) memory is exhausted.

Even if the wasted memory is not critical for the application at hand, when we write high-quality scientific software, memory leaks are unacceptable. When many people are using our software, sooner or later somebody will criticize us for it and eventually discourage other people from using our software. Fortunately, there are tools to help you to find memory leaks, as demonstrated in Section B.3.