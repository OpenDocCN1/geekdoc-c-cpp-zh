# Appendix G Selected Library Functions

# The <cassert> Facility

The assert facility from <cassert> can be used by writing a statement of the form:

```
assert(expression);
```

Notice that assert is not part of the std namespace (the name is simply assert, rather than std::assert). If the expression is true, then the assertion does no action. If the expression is false, then the assertion prints an error message that includes the text of the expression and stops the program.

For example, consider this assertion:

```
assert(i > 0);
```

If i is positive, then the assertion does nothing. If i is nonpositive, then the assertion will print a message such as “Assertion failed on line 42: i > 0”. The primary purpose of using such assertions is to aid a programmer in finding errors at the earliest possible moment.

Once a program is no longer undergoing testing, a programmer can turn off all assertions by placing the following at the top of each file:

```
#define NDEBUG
```

# Functions from <ctype> to Manipulate Characters

```
isalpha(c); // Returns true if c is a letter from 'A' to 'Z' or from 'a' to 'z'.
islalnum(c); // Returns true if c is a letter from 'A' to 'Z' or 'a' to 'z', or a digit from '0' to '9'.
isdigit(c); // Returns true if c is a digit from '0' to '9'.
isspace(c); // Returns true if c is a blank, tab, newline, or carriage return.
tolower(c); // If c is an uppercase letter, then the function returns the equivalent lowercase letter. Otherwise c is returned unchanged.
toupper(c); // If c is a lowercase letter, then the function returns the equivalent uppercase letter. Otherwise c is returned unchanged.
```

# Random Number Facility from <cstdlib>

```
int rand(); // Successive calls to rand() return a sequence of // pseudorandom numbers in the range 0 to RAND_MAX.
void srand(unsigned int seed); // The seed for the pseudorandom number generator // has been set to the specified value.
const int RAND_MAX; // The largest return value from the rand function
```