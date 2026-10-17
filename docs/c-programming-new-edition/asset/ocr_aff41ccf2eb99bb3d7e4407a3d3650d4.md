# 6.3. POINTER VARIATIONS

You will now dig deep into the different pointer variations that are up on offer. There are basically three types of pointer variations that are described by C.

They are:

+   - Pointer declaration;
+   - Pointer arithmetic;
+   - Pointer comparisons.

Each of the above variations has a story to tell but the discussion will be limited to what is pertaining to your up gradation of knowledge about pointers. Pointer Declaration If you are thinking that this is yet another declaration, this is nowhere remotely near the earlier ones.

The pointer declaration or it can be called pointer assignment, is where the address of a particular variable is assigned or initialized to another variable. That is to say the value of a variable will be the address of another variable. Consider the following example x=&y; In the above depiction the address of y is the value of x that is, if the address of y is 2457 and the assignment is done then the value of x will also be 2457.

But the variable x has to be declared before it can actually be used. If there is still a doubt in your mind the graphic representation below should erase it. Address of x, y is 8123 and 2457.

If the addresses have to be entered into a variable the variable should be declared in a particular manner after the main. Take a look below. 2457 5 int *x; That is how the pointer variables are declared. The above declaration tells the compiler that the variable x is being used to store an address of another variable and thus variables declared of this type can be used only to store addresses and nothing else. These are called pointer variables and each pointer variable should be preceded by a * operator along with the specification of data type.

Pointer Arithmetic When referring to arithmetic your area of concern will be to study if arithmetic can be incorporated into the concept of pointers and if yes to what extent is arithmetic valid in pointers. It is sad declaring the fact that in pointers only addition and subtraction operations can be performed and apart from this nothing else.