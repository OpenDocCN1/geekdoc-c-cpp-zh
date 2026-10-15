# ## 11.6 Overloading Unary Operators

A unary operator for a class can be overloaded as a non-static member function with no arguments or as a global function with one argument; that argument must be either an object of the class or a reference to an object of the class. Member functions that implement overloaded operators must be non-static so that they can access the non-static data in each object of the class. Remember that static member functions can access only static members of the class.

Later in this chapter, we’ll overload unary operator ! to test whether an object of the String class we create (Section 11.10) is empty and return a bool result. Consider the expression !s, in which s is an object of class String. When a unary operator such as ! is overloaded as a member function with no arguments and the compiler sees the expression !s, the compiler generates the function call s.operator!(). The operand s is the class object for which the String class member function operator! is being invoked. The function is declared in the class definition as follows:

```
class String
{
public:
   bool operator!() const;
   ...
}; // end class String
```

A unary operator such as ! may be overloaded as a global function with one parameter in two different ways—either with a parameter that is an object (this requires a copy of the object, so the side effects of the function are not applied to the original object), or with a parameter that is a reference to an object (no copy of the original object is made, so all side effects of this function are applied to the original object). If s is a String class object (or a reference to a String class object), then !s is treated as if the call operator!() had been written, invoking the global operator! function that is declared as follows:

```
bool operator!( const String & );
```

# ## 11.7 Overloading Binary Operators

A binary operator can be overloaded as a non-static member function with one parameter or as a global function with two parameters (one of those parameters must be either a class object or a reference to a class object).

Later in this chapter, we’ll overload < to compare two String objects. When overloading binary operator < as a non-static member function of a String class with one argument, if y and z are String-class objects, then y < z is treated as if y.operator<(z) had been written, invoking the operator< member function declared below

```
class String

public:
   bool operator<( const String & ) const;

}; // end class String
```

If binary operator < is to be overloaded as a global function, it must take two arguments—one of which must be a class object or a reference to a class object. If y and z are