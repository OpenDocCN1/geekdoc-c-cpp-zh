files as the left-hand side operand to the insertion operator. In such cases, the values on
right stored in the associated files.

# 1.5.2 Console Input

The input functions in C language, such as scanf(), can be included in C++ programs because
they are anyway defined in the standard library. However, we do have some ways of
inputting from the console in C++. Let us consider an example.

+   Listing 1.12 Inputting in C++

```
/*Beginning of iostream.cpp*/
#include<iostream.h>
void main()
{
    int x;
    cout<<"Enter a number: ";
    cin>>x; //console input in C++
    cout<<"You entered: "<<x;
}
/End of cin.cpp*/
```

# Output

Enter a number: 10<enter>
you entered: 10

The third statement in the main() function of Listing 1.12 needs to be understood.
cin (pronounce see-in) is actually an object of the class istream_withassign (you can
think of it as an alias of the structure istream_withassign. It stands as an alias for the
console input device, that is, the keyboard (hence the name).

The >> symbol, originating the right-shift operator, has had its definition extended in C++.
In the given context, it operates, as the extraction operator. It is a binary operator and takes
two operands. The operand on its left must be some object of the istream_withassign.
The operand on its right must be a variable of some fundamental data type. The value for
variable on the right of the extraction operator is extracted (hence the name) from the
istream originating from the device associated with the object on the left. Consequently, the
value of 'x' is obtained from the keyboard.

The file iostream.h needs to be included in the source code to ensure successful compilation
because the object cin and the extraction operator have been declared in that file.

Again, just like the insertion operator, the extraction operator works equally well
with variables of all fundamental types as its right-hand operand. It does not need the format
specifiers that the scanf() family of functions. Listing 1.13 exemplifies this.

+   Listing 1.13 Inputting data with the extraction operator

```
/*Beginning of cin.cpp*/
#include<iostream.h>
void main()
{
    int iVar;
```