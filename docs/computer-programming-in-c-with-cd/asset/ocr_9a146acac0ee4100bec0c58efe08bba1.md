Table 2 describes operators that cannot be overloaded:

| Table 2: Operators Cannot Be Overloaded |  |
|---|---|
| **Operator** | **Description** |
| `.` | The direct member selection operator |
| `.*` | The de-reference pointer to class member operator |
| `?:` | The conditional operator |
| `::` | The scope resolution operator |
| `sizeof` | The sizeof operator |

Table 3 lists operators that should not be overloaded, because they destroy the meaning of the built-in operators:

| Table 3: Operators Not To Be Overloaded |  |
|---|---|
| **Operator** | **Description** |
| `&&` | The AND logical operator |
| `||` | The OR logical operator |
| `,` | The comma operator |

Some important points that must be followed when performing operator overloading are:

+   - Only existing operators can be overloaded.
+   - The overloaded operators must have at least one operand, that is of user-defined type.
+   - You cannot change the meaning of an operator. It means, you cannot redefine the addition operator (`+`) to subtract one value from the other.
+   - Overloaded operators follow the syntax rules of the original operators that cannot be overridden.
+   - You cannot use friend functions to overload certain operators. Table 4 lists the operators that cannot be overloaded with friend functions:

| Table 4: Operators that Cannot Be Overloaded with Friend Functions |  |
|---|---|
| **Operators** | **Description** |
| `=` | Assignment operator |
| `()` | Function call operator |
| `[]` | Subscripting operator |
| `->` | Class member access operator |

Let’s perform the following tasks by using the operator keyword:

+   - Overloading of unary operators
+   - Overloading of increment (`++`) operators
+   - Overloading of unary operator returning object