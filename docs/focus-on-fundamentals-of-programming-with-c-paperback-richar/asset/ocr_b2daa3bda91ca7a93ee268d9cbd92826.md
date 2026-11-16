# # Pointers Homework

1. If x is a variable and p is a pointer to x, which of the following expressions are aliases for x?

a) *p		c) *&p		e) *x		g) *&x
b) &p		d) &*p		f) &x		h) &*x

2. If x is an int variable and p and q are pointers to int, which of the following assignments are legal?

a) p = x		d) p = &q		g) p = *q
b) *p = &x		e) p = *&q		h) *p = q
c) &p = q		f) p = q		i) *p = *q

3. Write a line of code for each of the examples below. Assume that num1 and num2 are int variables and num1 is initialized to 5.

a) Define variable p to be a pointer to an int.

b) Assign the address of num1 to pointer p.

c) Print the value of the variable pointed to by p.

d) Assign the value of the variable pointed to by p to variable num2.

e) Print the value of num2.

4. Suppose that the following declarations are in effect:

int a[] = { 5, 15, 34, 54, 14, 2, 52, 72 };
int *p = &a[1];
int *q = &a[5];

a) What is the value of * (p + 3) ?

b) What is the value of * (q - 3) ?

c) What is the value of q - p?