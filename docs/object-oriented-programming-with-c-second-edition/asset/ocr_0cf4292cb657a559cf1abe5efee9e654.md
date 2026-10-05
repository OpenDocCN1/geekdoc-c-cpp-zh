```
void main() 
{
    Distance * dptr;
    dptr = new Distance(1
```

# Output

I.1.

The first line of the function main() in Listing 4.5 and the second line of the main() function in Listing 4.6 show the syntax for passing values to the parameterized constructor. The parameterized constructor is prototyped and defined just like other member function except for the fact that it does not return any value.
ust remember that if the parameterized constructor is provided and the zero-argument constructor is not provided, the compiler will not provide the default constructor. In such a case, the following statement will not compile.

Distance d1; //ERROR: No matching constructor

Just like other member functions, the formal arguments of the parameterized constructor can be assigned default values. But that case, the zero-argument constructor should be provided. Otherwise, an ambiguity error will arise when we attempt to create an object without passing any values for the constructor. See Listing 4.7.

**Listing 4.7** Default values given to parameters of a parameterized constructor make the zero-argument constructor unnecessary

```
/*Beginning of Distance.h*/
class Distance {
public:
    ~Distance();//zero-argument constructor commented out
    Distance(int=0,float=0.0);    //default values given
    /*
    rest of the class Distance
    */
};
/*/End of Distance.h*/
```

We write,
Distance d1;

an ambiguity error arises if the zero-argument constructor is also defined. This is because both the zero-argument constructor and the parameterized constructor can resolve this statement.

Let us now create a parameterized constructor for the class String. We will also assign a default value for the argument of the parameterized constructor. The constructor would handle the following statements.

String s1("abc");
OR