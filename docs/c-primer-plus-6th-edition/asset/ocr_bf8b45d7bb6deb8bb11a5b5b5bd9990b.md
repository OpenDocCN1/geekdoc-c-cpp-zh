Output with cout 1071

cout << name;
cout << pn;

The methods use the terminating null character in the string to determine when to stop displaying characters.
C++ matches a pointer of any other type to void * and prints a numeric representation of the address. If you want the address of the string, you have to type cast it to another type, as shown in the following code fragment:

```
int eggs = 12;
char * amount = "dozen";
cout << &eggs; // prints address of eggs variable
cout << amount; // prints the string "dozen"
cout << (void *)amount; // prints the address of the "dozen" string
```

# Output Concatenation

All the incarnations of the insertion operator are defined to return type ostream.That is, the prototypes have this form:
ostream & operator<<(type);

(Here, type is the type to be.) The ostream & return type means that using this operator returns a reference to an ostream object. Which object? The definition says that the reference is to the object used to evoke the operator. In other words, an operator function's return value is the same as that evokes the operator. For example, cout << "potluck" returns the cout object. That's the feature that lets you concatenate output by using insertion. For example, consider the following statement:

cout << "We " << count << " unhatched chickens.\n";

The expression count << "We " displays the string and the count object, reducing the statement to the following:
cout << count << " unhatched chickens.\n";

Then the expression count << count displays the value of the count variable and returns count, which can then handle the final argument in the statement (see Figure 17.4).This design technique is a nice feature, which is the examples of overloading the << operator in the previous chapters shamelessly imitate it.

# The Other ostream Methods

Besides the various operator<<() functions, the ostream class provides the put() method for displaying characters and the write() method for displaying strings.