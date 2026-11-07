# **Program 7.10** The fraction.h file (Continued)

```
~~~cpp
12  // Data members
13  private:
14      int numer;
15      int denom;
16
17  // Public member functions
18  public:
19      // Constructors
20      Fraction (int num, int den);
21      Fraction ();
22      Fraction (const Fraction& fract);
23      ~Fraction ();
24      // Accessors
25      int getNumer () const;
26      int getDenom () const;
27      void print () const;
28      // Mutators
29      void setNumer (int num);
30      void setDenom (int den);
31
32      // Helping private member functions
33  private:
34      void normalize ();
35      int gcd (int n, int m);
36  };
37  #endif
~~~
```

to handle the class invariants (*normalize* and *gcd*). They are declared private so that they are only accessible through the class parameter constructor.

# **Implementation File**

We now write the function definition for all member functions (*public* and *private*) defined in the interface file. Note that we have added the interface file as a header file in this program (the compiler needs to see the declarations before compiling the definitions). **Program 7.11** shows the implementation file.

+   - We have added the `<cassert>` header file in line 7 to allow the use of the *assert* macro in line 101, which is needed to abort the program if the denominator is 0.
+   - Lines 104 to 108 take care of second condition of the class invariant. If the denominator is negative, we change both numerator and denominator to move the negative sign to the numerator.
+   - Lines 110 to 112 take care of the third condition of the class invariant. We use the greatest common divisor function, as discussed in previous chapters, to find the greatest divisor between numerator and denominator and then divide both by this divisor. Note that we use the absolute values of numerator and denominator when computing *gcd*.