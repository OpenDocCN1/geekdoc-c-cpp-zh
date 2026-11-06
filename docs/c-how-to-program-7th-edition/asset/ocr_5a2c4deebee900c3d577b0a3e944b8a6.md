```
```cpp
21     
22     // print x using implicit and explicit this pointers;
23     // the parentheses around *this are required
24     void Test::print() const
25     {
26       // implicitly use the this pointer to access the member x
27       cout << " x " << x << endl;
28
29       // explicitly use the this pointer and the arrow operator
30       // to access the member x
31       cout << " x " << this->x << " x " << this->x;
32
33       // explicitly use the dereferenced this pointer and
34       // the dot operator to access the member
35       cout << "\n(*this).x " << (*this).x << endl;
36     } // end function print
37
38     int main()
39     {
40       Test testObject( 12 ); // instantiate and initialize testObject
41
42       testObject.print();
43     } // end main

     x = 12
     this->x = 12
     (*this).x = 12
```
```

**Fig. 10.16 |** this pointer implicitly and explicitly accessing an object's members. (Part 2 of 2.)

For illustration purposes, member function `print` (lines 24–36) first prints x by using the `this` pointer implicitly (line 27)—only the name of the data member is specified. Then `print` uses two different notations to access x through the `this` pointer—the arrow operator (`->`) off this pointer (line 31) and the dot operator (`.`) off the dereferenced this pointer (line 35). Note the parentheses around `*this` (line 35) when used with the dot member selection operator (`.`). The parentheses are required because the dot operator has higher precedence than the `*` operator. Without the parentheses, the expression `*this.x` would be evaluated as if it were parenthesized as `*(this.x)`, which is a compilation error, because the dot operator cannot be used with a pointer.

> **Common Programming Error 10.7**
> 
> *Attempting to use the member selection operator (.) with a pointer to an object is a compilation error—the dot member selection operator may be used only with an lvalue such as an object's name, a reference to an object or a dereferenced pointer to an object.*

One interesting use of the `this` pointer is to prevent an object from being assigned to itself. As we’ll see in Chapter 11, self-assignment can cause serious errors when the object contains pointers to dynamically allocated storage.

# *Using the this Pointer to Enable Cascaded Function Calls*

Another use of the `this` pointer is to enable cascaded member-function calls—that is, invoking multiple functions in the same statement (as in line 12 of Fig. 10.19). The program