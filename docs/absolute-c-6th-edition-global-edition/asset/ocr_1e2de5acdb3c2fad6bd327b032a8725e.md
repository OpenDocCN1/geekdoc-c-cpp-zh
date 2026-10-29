# using Declarations

This subsection describes a way to qualify a single name so that you can make only one name from a namespace available to your program, rather than making all the names in a namespace available. We saw this technique in Chapter 1 and so this is a review and amplification of what we said in Chapter 1.

Suppose you are faced with the following situation. You have two namespaces, NS1 and NS2. You want to use the function fun1 defined in NS1 and the function fun2 defined in namespace NS2. The complication is that both NS1 and NS2 define a function myFunction. (Assume all functions in this discussion take no arguments, so overloading does not apply.) You cannot use

```
using namespace NS1;
using namespace NS2;
```

This would potentially provide conflicting definitions for myFunction. (If the name myFunction is never used, the compiler will not detect the problem and will allow your program to compile and run.)

What you need is a way to say you are using fun1 in namespace NS1 and fun2 in namespace NS2 and nothing else in the namespaces NS1 and NS2. We have already been using a technique that can handle this situation. The following is your solution:

```
using NS1::fun1;
using NS2::fun2;
```

A qualification of the form

```
using Name_Space::One_Name;
```

makes (the definition of the) name One_Name from the namespace Name_Space available, but does not make any other names in Name_Space available. This is called a using declaration.

Note that the scope resolution operator :: that we use in these using declarations is the same as the scope resolution operator we use when defining member functions. These two uses of the scope resolution operator have a similarity. For example, Display 11.2 had the following function definition:

```
void DigitalTime::advance(int hoursAdded, int minutesAdded)
{
    hour = (hour + hoursAdded)%24;
    advance(minutesAdded);
}
```

In this case the :: means that we are defining the function advance for the class DigitalTime, as opposed to any other function named advance in any other class. Similarly,

```
using NS1::fun1;
```

means we are using the function named fun1 as defined in the namespace NS1, as opposed to any other definition of fun1 in any other namespace.