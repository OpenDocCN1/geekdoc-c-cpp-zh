
# Chapter 4 Compound Types

```
cout << "ps = " << ps << ", *ps = " << ps << endl;
ps = ps + 1;
cout << "add 1 to the ps pointer:\n";
cout << "ps = " << ps << ", *ps = " << ps << "\n\n";

cout << "access two elements with array notation\n";
cout << "*stacks[0] = " << stacks[0];
cout << ", * stacks[1] = " << stacks[1] << endl;
cout << "access two elements with pointer notation\n";
cout << "*stacks = " << *stacks;
cout << ", * *(stacks + 1) = " << *(stacks + 1) << endl;

cout << sizeof(pw) << " = " << size of wages array\n";
cout << sizeof(pw) << " = " << size of pw pointer\n
```

Here is the output from the program in Listing 4.19.

```
pw = 0x28ccf0, *pw = 10000
add 1 to the pw pointer:
pw = 0x28ccf8, *pw = 20000

ps = 0x28ccea, *ps = 3
add 1 to the ps pointer:
ps = 0x28cccec, *ps = 2
```

```
access two elements with array notation
stacks[0] = 3, stacks[1] = 2
access two elements with pointer notation
*stacks = 3, * *(stacks + 1) = 2
24 = size of wages array
4 = size of pw pointer
```

## Program Notes

In many contexts, C++ interprets the address of an array as the address of its first element. Thus, the following statement makes pw a pointer to type double and then initializes pw to wages, which is the address of the first element of the wages array:

```
double *pw = wages;
```

For wages, as with any array, we have the following equality:

```
wages = &wages[0] = address of first element of array
```

Just to show that this is no joke, the program explicitly uses the address operator in the expression &stacks[0] to initialize the ps pointer to the first element of the stacks array.

## Pointers, Arrays, and Pointer Arithmetic 169

Next, the program inspects the values of pw and *pw. The first is an address, and the second is the value at address. Because pw points to the first element, the value displayed for *pw is that of the first element, 10000. Then the program adds one to pw. As promised, this adds eight to the numeric value because double on this system is 8 bytes. This pw equal to the address of the second element. Thus, *pw is now 20000, the value of the second element (see Figure 4.10). The addresses in the figure are adjusted to match the wider [.]

```
double wages[3] = {10000.0, 20000.0, 30000.0};
short stacks[3] = {3, 2, 1};
double * pw = wages;
short * ps = &stacks[0];
```

![](img/cd111a87c1db9aff4db4b18834327463_183_0.png)

After this, the program goes through similar steps for ps. This time, because ps points to type short and short is 2, adding 1 to the pointer increases its value by 2 (0x28cca + 2 = 0x28cec in hexadecimal). Again, the result is to make the pointer point to the next element of the array.

> Note: Adding one to a pointer variable increases its value by the number of bytes of the type to it points.

Now consider the array expression stacks[1]. The C++ compiler treats this expression as if you wrote it as *(stacks + 1). The second means calculate the address of the second element and then finds the value there. The result is precisely what stacks[1] means.(Operator precedence requires that you use the parentheses. Without them, it would be added to *stacks instead of stacks).
The program output demonstrates that *(stacks + 1) and stacks[1] are the same. Similarly, *(stacks + 2) is the same as stacks[2]. In general, wherever you use array notation, C++ makes the following conversion:
arrayname[i] becomes *(arrayname + i)

## Chapter 4 Compound Types

And if you use a pointer instead of an array name, C++ makes the same conversion: pointername[i] becomes *pointername + i

Thus, in many respects you can use pointer names and array names in the same way.
You can use the array brackets with neither.You can use the dereferencing operator (*) to either. In most expressions, each expression represents an address. One difference is that you can change the value of a pointer, whereas an array name is a constant:

```
pointername = pointername + 1; // valid
arrayname = arrayname + 1; // not allowed
```

A difference is that applying the sizeof operator to an array name yields the size of the array, but applying to a pointer yields the size of the pointer, even if the pointer points to the array. For example, in Listing 4.9, both pw and wages refer to the same array. By applying the sizeof operator to them produces the following results:

```
24 = size of wages array << displaying wages
4 = size of pw pointer << displaying pw
```

This is one case in which C++ does not interpret the array name as an address.

## The Address of an Array

Taking the address of an array is another case in which the name of an array is not interpreted as its address. But wait, isn't the name of the array interpreted as the address of the array? Not quite—the name of the array is interpreted as the address of the first element of an array, whereas applying the address operator yields the address of the whole

```
short tell[10]; // tell an array of 20 bytes
cout << &tell << endl; // displays &tell[0]
cout << &tell << endl; // displays address of whole array
```

Numerically, these two addresses are the same, but conceptually &tell, and hence tell, is the address of a 2-byte block of memory. The expression +1 adds 2 to the address value, whereas &tell + 1 adds 20 to the address value. Another way of explaining this is to say tell is type-to-short, or short *, and &tell is type-to-array-of-20-shorts, or short (*) [20].

Now you might be wondering about the genesis of that type description. First, here is you could declare and initialize a pointer of that:

```
short (*pas) = &tell; // pas points to array of 20 shorts
```

If you omit the parentheses, precedence rules would associate [20] with pas, making an array of 20 pointers-to-short, so the parentheses are necessary. Next, if you wish to describe the type of a variable, you can use the declaration of that variable as a guide and remove the variable name. Thus, the type of pas is short (*) [20]. Also note that because pas is set to &tell, *pas is equivalent to tell, so (*pas) [20] would be the first element of the tell array.

In short, using new to create an array and a pointer to access the different elements is a simple matter. You just treat the pointer as an array name. Understanding why this works, is an interesting challenge. If you actually want to understand arrays and pointers, you should review their mutual relationships carefully.

## Summarizing Pointer Points

You've been exposed to quite a bit of pointer knowledge lately, so let's summarize what's been revealed about pointers and arrays to date.

### Declaring Pointers

To declare a pointer to a particular type, use this form:

```
typeName * pointerName;
```

Here are some examples:

```
double * pn;              // pn can point to a double value
char * pc;               // pc can point to a char value
```

Here pn and pc are pointers, double * and char * are the C++ notations for the types pointer-to-double and pointer-to-char.

### Assigning Values to Pointers

You should assign a memory address to a pointer. You can apply the & operator to a variable to get an address of named memory, and the new operator returns the address of unnamed memory.

Here are some examples:

```
double * pn;              // pn can point to a double value
double * pa;              // so can pa
char * pc;               // pc can point to a char value
double bubble = 3.2;      // assign address of bubble to pn
pn = &bubble;             // assign address of newly allocated char memory to pc
c = new char;
pa = new double[30];    // assign address of 1st element of array of 30 to pa
```

### Dereferencing Pointers

Dereferencing a pointer means referring to the pointed-to-value. You apply the dereferencing, or indirect value, operator (*) to a pointer to dereference it. Thus, if pn is a pointer to bubble, as in the preceding example, then *pn is the pointed-to-value, or 3.2, in this case.

Here are some examples:

```
cout << *pn;      // print the value of bubble
*pc = 'S';               // place 'S' into the memory location whose address is pc
```
