# The statement

```
```cpp
p = q;
```
```

copies the value of q into p. After this statement executes, both p and q point to the same memory location. Any changes made to *p automatically change the value of *q, and vice versa.

Two pointer variables of the same type can be compared for equality, and so on. The expression

```
```cpp
p == q
```
```

evaluates to true if p and q have the same value—that is, if they point to the same memory location. Similarly, the expression

```
```cpp
p != q
```
```

evaluates to true if p and q point to different memory locations.

Integer values can be added and subtracted from a pointer variable. The value of one pointer variable can be subtracted from another pointer variable. The arithmetic operations that are allowed differ from the arithmetic operations on numbers. First, let us use the following statements to explain the increment and decrement operations on pointer variables:

```
```cpp
int *p;
double *q;
char *chPtr;
studentType *stdPtr;    //studentType is as defined before
```
```

Recall that the size of the memory allocated for an int variable is 4 bytes, a double variable is 8 bytes, and a char variable is 1 byte. The memory allocated for a variable of type studentType is then 40 bytes.

# The statement

```
```cpp
p++ or p = p + 1;
```
```

increments the value of p by 4 bytes because p is a pointer of type int. Similarly, the statements

```
```cpp
q++;
chPtr++;
```
```

increment the value of q by 8 bytes and the value of chPtr by 1 byte, respectively. The statement

```
```cpp
stdPtr++;
```
```

increments the value of stdPtr by 40 bytes.

The increment operator increments the value of a pointer variable by the size of the data type or structure to which it is pointing. Similarly, the decrement operator decrements the value of a pointer variable by the size of the data type or structure to which it is pointing.