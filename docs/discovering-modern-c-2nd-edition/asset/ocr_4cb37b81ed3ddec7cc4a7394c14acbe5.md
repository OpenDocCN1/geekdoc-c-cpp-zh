```
12:36: instantiated from >>void Prime_print<i>::f() [with int i = 13]<<
12:36: instantiated from >>void Prime_print<i>::f() [with int i = 14]<<
12:36: instantiated from >>void Prime_print<i>::f() [with int i = 15]<<
12:36: instantiated from >>void Prime_print<i>::f() [with int i = 16]<<
12:36: instantiated from >>void Prime_print<i>::f() [with int i = 17]<<
12:36: instantiated from >>void Prime_print<i>::f() [with int i = 18]<<
25:6: instantiated from here
12:33: error: invalid conversion from >>int<< to >>void*<<
12:33: error: initializing argument 1 of >>D<i>::D(void*)<<
[with int i = 11]<<
In member function >>void Prime_print<i>::f() [with int i = 7]<<
12:36: instantiated from >>void Prime_print<i>::f() [with int i = 8]<<
... message continues
```

When we filter this for initializing,11 we see clearly how well our compiler computes:

11. With bash: make unruh 2>&1 | grep initializing; with tcsh: make unruh |& grep initializing.

# Click here to view code image

```
12:33: error: initializing argument 1 of >>D<i>::D(void*)<<
[with int i = 17]<<
12:33: error: initializing argument 1 of >>D<i>::D(void*)<<
[with int i = 13]<<
12:33: error: initializing argument 1 of >>D<i>::D(void*)<<
[with int i = 11]<<
12:33: error: initializing argument 1 of >>D<i>::D(void*)<<
[with int i = 7]<<
12:33: error: initializing argument 1 of >>D<i>::D(void*)<<
[with int i = 5]<<
12:33: error: initializing argument 1 of >>D<i>::D(void*)<<
[with int i = 3]<<
12:33: error: initializing argument 1 of >>D<i>::D(void*)<<
[with int i = 2]<<
```