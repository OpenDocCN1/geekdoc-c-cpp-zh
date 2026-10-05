# Operator Overloading, Type Conversion, New Style Casts, and RTTI

```
;
(<param_list>);

//definition
<return_type> operator <rel_op_symbol> (<param_list>)
{
    //function body
}
```

Objects that store the values of both the left-hand side and the right-hand side operands of the relational operator will appear in the list of formal arguments.
The

Obj1 <rel_op_symbol> Obj2
 be interpreted as

```
Obj1.operator <rel_op_symbol>(Obj2)
```

Since, the relational operator has been overloaded through a friend function, the\interpretation will be

```
operator <rel_op_symbol> (Obj1,Obj2)
```

Now, let us find out how to overload the greater than relational operator for the class
Distance. We would like to use this piece of code given in Listing 8.25 to compile successfully
and its output to be "Greater".

# 8.25 Using an overloaded greater operator for the class Distance

```
Distance d1(5,8),d2(4,6);
if(d1>d2)
    cout<<"Greater than";
else
    cout<<"Less than";
```

For this, we must overload the 'greater than' operator for the class Distance by
either a member function or a friend function.
Let us look at a member function to overload the greater operator for the class
Distance. In this case, the expression

```
d1>d2
d1.operator(d2)
```

be interpreted as
Obviously, the function must return a boolean-type value (true or false) and should accept
an object of the class Distance as a parameter. The actual code to implement the greater
than operator so that it produces the aforementioned effect is given in Listing 8.26.

+   8.26 Overloading the greater operator for the class Distance through a
member function

```
/*Beginning of Distance.h*/
enum bool{false, true};
class Distance
```