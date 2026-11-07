```
Program 15.1 Using three overloaded functions (Continued)

37 cout << "Smaller of 'a' and 'B': " << smaller ('a', 'B') << endl;
38 cout << "Smaller of 12 and 15: " << smaller (12, 15) << endl;
39 cout << "Smaller of 44.2 and 33.1: " << smaller (44.2, 33.1) << endl;
40 return 0;
41 }

Run:
Smaller of 'a' and 'B': B
Smaller of 12 and 15: 12
Smaller of 44.2 and 33.1: 33.1
```

Writing three similar functions can be avoided if we use templates and write only one function.

# 15.1.2 Using Function Template

We first give the syntax of a function template to be defined and then the concept of instantiation, which is the way the compiler handles instantiations.

# Syntax

To create a template function, we can use a placeholder for each generic type. Table 15.1 shows the general syntax for a generic function, in which T, U, ..., and Z are replaced by actual types when the function is called.

As shown in Table 15.1, the template header contains the keyword template followed by a list of symbolic types inside two angle brackets. The template function header follows the rules for function headers except that the types are symbolic as declared in the template header. While multiple generic types are possible, a function template with more than two generic types is rare. Some older code uses the term class rather than typename. We use the keyword typename because it is the current standard and is used in the C++ library.

We change Program 15.1 using a function template as shown in Program 15.2. In this program we have only one generic type, but the type is used three times: twice as parameters and once as the return type. In this program the type of the parameters and the returned value are the same.

We can see that the result is the same as in Program 15.1. We have saved code by writing only one template function instead of three overloaded functions. Note that we have

| Table 15.1 Syntax of a template function |
| --- |
| template <typename T, typename U, ..., typename Z><br>T functionName (U first, ... Z last)<br>{<br>  ...<br>} |