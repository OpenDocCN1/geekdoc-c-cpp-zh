Consider the following sample personal details needs to be filled in, for example, the variable declaration for the considered common personal details can be expressed as;

| Equivalent variable declaration | Required to fill personal details in some real world situation |
|---|---|
| char[35] name;
int age;
float weightInKgs ;
boolean personalLoan ;
char gender; | Name : ........................
Age : ........................
Weight(In Kgs) : ........................
Personal loan (true/false): ....................
Gender(M/F) : ........................ |

For example, the data value 25 could be an age, price and there are many more possibilities. The name of variable should be appropriately chosen by giving full idea about the data it is going to refer. The chosen name of variable helps us to know meaning of stored value contained in it.

# How to store data/value in a variable?

Yes, it is made possible through the facility of variable assignment using assignment operator (=)

# Variable assignment

The format for variable assignment is as follows:

```
data_type variable_name = data; // assign only one data at a time
```

+   - variable_name represents a memory address and also known as lvalue.
+   - data value on the right-hand side of an assignment operator (=) is rvalue.

| CONCEPTUAL LAYOUT OF A VARIABLE |  |  |
|---|---|---|
| data-type | variable_name = | Data within the range of data-type (rvalue) |
|  |  | Memory Address (lvalue) |

Any real time situation of manually filling data can be simulated using feature of a programming language known as variable assignment. Variable assignment is a simple act of storing an appropriate value in an appropriate variable. We can assign the value to the variable using assignment operator (=).The value of a variable can be over-written programmatically and that is why it's called variable. In a class room, the space of board are re-used by wiping out the details for every new class. In the similar way these variables can be over-written programmatically during the course of running/executing the program. We can store or assign only one data at a time.

Every single programming statement is separated by ';', similarly like how a full-stop (.) separates each sentence in a proper textual information.

| Equivalent variable assignment | Filled in personal details |
|---|---|
| char[35] name = "James Arthur Gosling";
int age = 63 ;
float weightInKgs = 53.6f;
boolean personalLoan = false;
char gender = 'M'; | Name : James Arthur Gosling
Age: 63
Weight(In Kgs) : 53.6
Personal loan (true/false): false
Gender : M |

The names of variables represents memory locations. It is very difficult to do programming using name of memory locations. Memory location address resembles not less than any secret key. The name of a variable that we choose should be a user-friendly name which represents a specific memory location allocated for the purpose to store data.