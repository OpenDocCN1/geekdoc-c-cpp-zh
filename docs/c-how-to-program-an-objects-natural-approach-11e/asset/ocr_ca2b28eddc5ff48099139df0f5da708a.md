Interfaces typically do not have data members. Interface inheritance may require more work than implementation inheritance because concrete classes must provide both data and implementations of the interface's pure virtual member functions, even if they're similar or identical among classes. As we'll discuss at the end of the example, this approach gives you additional flexibility by eliminating the tight coupling between classes. The discussion of device drivers in the context of abstract classes at the end of Section 10.8 is a good example of how interfaces enable systems to be modified easily.

# ### 10.11.1 Rethinking the Employee Hierarchy—CompensationModel Interface

Let's refactor Section 10.9's `Employee` hierarchy with composition and an interface. We can say that each `Employee` has a `CompensationModel`. Figure 10.19 defines the interface `CompensationModel`, which is a pure abstract class, so it does not have a `.cpp` file. The class has a compiler-generated virtual destructor and two pure virtual functions:

+   - `earnings` to calculate an employee's pay based on its `CompensationModel`, and
+   - `toString` to create a string representation of a `CompensationModel`.

Any class that inherits from `CompensationModel` and overrides its pure virtual functions is a `CompensationModel` that implements this interface.

```
~~~cpp
1  // Fig. 10.19: CompensationModel.h
2  // CompensationModel "interface" is a pure abstract base class.
3  #pragma once // prevent multiple inclusions of header
4  #include <string>
5
6  class CompensationModel {
7  public:
8     virtual ~CompensationModel() = default; // generated destructor
9     virtual double earnings() const = 0; // pure virtual
10    virtual std::string toString() const = 0; // pure virtual
11 };
~~~
```

**Fig. 10.19** | `CompensationModel` "interface" is a pure abstract base class.

# ### 10.11.2 Class Employee

Figure 10.20 defines our new `Employee` class. Each `Employee` has a pointer to the implementation of its `CompensationModel` (line 16). This class is declared `final`, so it cannot be used as a base class.

```
~~~cpp
1  // Fig. 10.20: Employee.h
2  // An Employee "has a" CompensationModel.
3  #pragma once // prevent multiple inclusions of header
4  #include <string>
5  #include <string_view>
6  #include "CompensationModel.h"
7
~~~
```

**Fig. 10.20** | An `Employee` "has a" `CompensationModel`. (Part 1 of 2.)