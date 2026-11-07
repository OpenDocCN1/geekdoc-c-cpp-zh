| Table 9.1 — Four possible combinations |  |  |  |
|---|---|---|---|
| **Case** | **Data variable** | **Reference variable** | **Status** |
| 1 | `int name = value;` | `int& rName = name;` | OK |
| 2 | `const int name = value;` | `int& rName = name;` | Error |
| 3 | `int name = value;` | `const int& rName = name;` | OK |
| 4 | `const int name = value;` | `const int& rName = name;` | OK |

The constant modifier can be put in front of the original variable or in front of the reference variable. The relationship (binding) is by nature constant and cannot be broken. Figure 9.5 shows the use of a const modifier for both the original and the reference variables.

Table 9.1 shows the four possible combinations, but the second one creates a compilation error, as we describe shortly.

# First Case

In the first case, there is no restriction to changing the value either through the original variable or through the reference variable.

# Second Case

The second case creates a compilation error because we try to bind a nonconstant reference variable to a constant variable. Since the original variable is already constant, there is now way that we can change its value through the reference variable.

# Third Case

In the third case, the data can be changed through the data variable, but we want to restrict it from being changed through the reference variable.

# Fourth Case

In the fourth case, we want to create an original variable and a reference variable in a way that neither the original variable nor the reference variable can change the common value. This case has little application because the data variable and the reference variable can only be used to retrieve data, not to change them.

# 9.1.4 Applications

Using references in the same namespace, such as in the same function, is unnecessary because we can always use the original variable instead of the reference variable. Both variables use the same memory location. The idea of references is beneficial when the two variables are in different scopes, like in a calling function and the called function. We can save memory by using one memory location and accessing it in two functions using the original variable and the reference variable.

In this section we discuss the use of references in the communication between two functions. We discuss using references in passing data to a function and in returning data from a function. The first application is called pass-by-reference; the second is called return-by-reference.