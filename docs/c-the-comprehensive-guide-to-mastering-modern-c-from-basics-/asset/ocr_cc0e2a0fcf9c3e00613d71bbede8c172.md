# What do the different print lines in main output in your opinion?

+   - Base ba{}; ba.print(cout);base call
In Base, the two print() and value() methods are defined directly. No other class is involved here.
value() returns eight_, and 8 is output.

+   - Print pr{}; pr.print(cout);print overridden
In Print, the print() method is overridden. For pr, the Print::print()method is called. value() is needed there. This method was inherited from Base. And
Base::value() returns eight\_so 8 is output.

+   - Value va{}; bo.print(cout)-print from Base
we.print() must fall back on the inherited method
Base::print(). Now the value() method is needed.
Although there is the value::value() method, it is not
yet known in Base::print()! In a method of the base
class, only methods of the base class are used—here,
Base::value(), which returns eight\_ and leads to the
output of 8.

+   - Both bo{}; bo.print(cout);-everything overwritten
Here is simple again: There is a Both::print() that
gets called. The call to value() accesses Both::value()
in its own method and refers to eleven\_ It outputs 11.

Did you correctly guess the third case? If not, don't be
upset. When value() method is taken by Base::print() is
matter of definition: both are possible. In C++, it is
defined such that a method only sees the methods
available at the time of the class's translation through