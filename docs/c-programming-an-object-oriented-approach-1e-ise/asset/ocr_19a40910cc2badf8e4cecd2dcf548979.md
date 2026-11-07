**Table 7.2** Class scope

| Group | Name | Operator | Expression | Pred | Assoc |
|---|---|---|---|---|---|
| Primary | class scope | `::` | `class :: name` | 19 | → |

The definition of each member function is similar to the definition that we have used in previous chapters, but with two differences. The first is the qualifier (`const`) that is applied to some member function. The second is the name of the function that must be qualified with the name of the class. This is similar to when we know two people with the same name. One coming from the Brown family and the other from the White family. In C++, we need to mention the class name (family name) first followed by a *class scope* (`::`) symbol to achieve this goal. The class scope is a primary expression as shown in Appendix C, but it is repeated in Table 7.2 for convenience.

You may ask why we did not include the last name of a data member or a member function in the class declaration. The reason is that these members are enclosed in the class definition; they belong to that class. This is similar to the case in which we do not mention the last name of an individual when she is in the family; the last name is used when we are out of the family circle. Figure 7.5 shows the difference.

Note that the return type of the function always comes before the whole name. In the class declaration, there is no explicit last name, so it comes before the first name. In the function definition, it must come before the whole name.

# 7.2.4 Inline Functions

When the body of a function is short, the execution time involved in the function call (storing the arguments, transferring control, retrieving the argument, and storing the return value) may be greater than executing the code inside the function. To improve program performance, we can declare a function as an **inline function** to indicate that the compiler can replace the function call with the actual code in the function. However, the compiler may ignore this request. We have not used inline functions in our previous programs and will not do so, but you are free to use this option.

# Implicit Inline Function

A function is defined as an **implicit inline function** when we replace its declaration (in the class definition) with its definition. This is not recommended for two reasons. First, it makes the definition more difficult to read. Second, it violates the principle of encapsulation, which we discuss shortly. The following shows a partial definition of the *Circle* class with an implicit inline function.

![](bbox=[0.338, 0.781, 0.825, 0.905])

**Figure 7.5** Using names in the class definition and member functions