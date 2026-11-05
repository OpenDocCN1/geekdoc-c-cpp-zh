
Initialization to default values is typically done by having the memory manager or garbage collector initialize memory to all-bits-zero before it is allocated for use. For this reason, it is convenient to use all-bits-zero to represent the null reference.

## 5.3 Definite Assignment

At a given location in the executable code of a function member, a variable is said to be definitely assigned if the compiler can prove, by a particular static flow analysis (§5.3.3), that the variable has been automatically initialized or has been the target of at least one assignment. Informally stated, the rules of definite assignment are:

- An initially assigned variable (§5.3.1) is always considered definitely assigned.
- An initially unassigned variable (§5.3.2) is considered definitely assigned at a given location if all possible execution paths leading to that location contain at least one of the following:
  - A simple assignment (§7.17.1) in which the variable is the left operand.
  - An invocation expression (§7.6.5) or object creation expression (§7.6.10.1) that passes the variable as an output parameter.
  - For a local variable, a local variable declaration (§8.5.1) that includes a variable initializer.

The formal specification underlying the above informal rules is described in §5.3.1, §5.3.2, and §5.3.3.

The definite assignment states of instance variables of a struct-type variable are tracked individually as well as collectively. In addition to the rules above, the following rules apply to struct-type variables and their instance variables:

- An instance variable is considered definitely assigned if its containing struct-type variable is considered definitely assigned.
- A struct-type variable is considered definitely assigned if each of its instance variables is considered definitely assigned.

Definite assignment is a requirement in the following contexts:

- A variable must be definitely assigned at each location where its value is obtained. This ensures that undefined values never occur. The occurrence of a variable in an expression is considered to obtain the value of the variable, except when
  - The variable is the left operand of a simple assignment,
  - The variable is passed as an output parameter, or
  - The variable is a struct-type variable and occurs as the left operand of a member access.
- A variable must be definitely assigned at each location where it is passed as a reference parameter. This ensures that the function member being invoked can consider the reference parameter initially assigned.
- All output parameters of a function member must be definitely assigned at each location where the function member returns (through a return statement or through execution reaching the end of the function member body). This ensures that function members do not return undefined values in output parameters, thus enabling the compiler to consider a function member invocation that takes a variable as an output parameter equivalent to an assignment to the variable.
- The this variable of a struct-type instance constructor must be definitely assigned at each location where that instance constructor returns.

### 5.3.1 Initially Assigned Variables

The following categories of variables are classified as initially assigned:

- Static variables.
- Instance variables of class instances.
- Instance variables of initially assigned struct variables.
- Array elements.
- Value parameters.
- Reference parameters.
- Variables declared in a catch clause or a foreach statement.

### 5.3.2 Initially Unassigned Variables

The following categories of variables are classified as initially unassigned:

- Instance variables of initially unassigned struct variables.
- Output parameters, including the this variable of struct instance constructors.
- Local variables, except those declared in a catch clause or a foreach statement.

### 5.3.3 Precise Rules for Determining Definite Assignment

To determine that each used variable is definitely assigned, the compiler must use a process that is equivalent to the one described in this section.

The compiler processes the body of each function member that has one or more initially unassigned variables. For each initially unassigned variable *v*, the compiler determines a *definite assignment state* for *v* at each of the following points in the function member:

- At the beginning of each statement.
- At the end point (§8.1) of each statement.
- On each arc that transfers control to another statement or to the end point of a statement.
- At the beginning of each expression.
- At the end of each expression.

The definite assignment state of *v* can be either:

- **Definitely assigned.** This indicates that on all possible control flows to this point, *v* has been assigned a value.
- **Not definitely assigned.** For the state of a variable at the end of an expression of type `bool`, the state of a variable that isn't definitely assigned may (but doesn't necessarily) fall into one of the following substates:
  - Definitely assigned after true expression. This state indicates that *v* is definitely assigned if the boolean expression evaluated as true, but is not necessarily assigned if the boolean expression evaluated as false.
  - Definitely assigned after false expression. This state indicates that *v* is definitely assigned if the boolean expression evaluated as false, but is not necessarily assigned if the boolean expression evaluated as true.

The following rules govern how the state of a variable *v* is determined at each location.

#### 5.3.3.1 General Rules for Statements

- *v* is not definitely assigned at the beginning of a function member body.
- *v* is definitely assigned at the beginning of any unreachable statement.

> **ERIC LIPPERT** This rule may strike you as unusual. Why should every variable be considered to be definitely assigned within an unreachable statement? Some reasons are discussed here.
>
> If the statement is unreachable, then it will not execute. If it will not execute, then it will not read from an unassigned variable. Therefore, it is not a problem; the compiler is looking for potential problems, and this is not one.
>
> Also, unreachable statements are almost certainly mistakes. Once the compiler has identified one mistake, odds are good that a whole host of related mistakes are clustered around it. Rather than reporting a huge number of related problems, it is often a better idea to report just one problem and allow the user to fix it, rather than trying to report every possible specification violation.

- The definite assignment state of *v* at the beginning of any other statement is determined by checking the definite assignment state of *v* on all control flow transfers that target the beginning of that statement. If (and only if) *v* is definitely assigned on all such control flow transfers, then *v* is definitely assigned at the beginning of the statement. The set of possible control flow transfers is determined in the same way as for checking statement reachability (§8.1).
- The definite assignment state of *v* at the end point of a block, checked, unchecked, if, while, do, for, foreach, lock, using, or switch statement is determined by checking the definite assignment state of *v* on all control flow transfers that target the end point of that statement. If *v* is definitely assigned on all such control flow transfers, then *v* is definitely assigned at the end point of the statement. Otherwise, *v* is not definitely assigned at the end point of the statement. The set of possible control flow transfers is determined in the same way as for checking statement reachability (§8.1).

#### 5.3.3.2 Block Statements, checked Statements, and unchecked Statements

The definite assignment state of *v* on the control transfer to the first statement of the statement list in the block (or to the end point of the block, if the statement list is empty) is the same as the definite assignment state of *v* before the block, checked, or unchecked statement.

#### 5.3.3.3 Expression Statements

For an expression statement stmt that consists of the expression expr:

- *v* has the same definite assignment state at the beginning of expr as at the beginning of stmt.
- If *v* is definitely assigned at the end of expr, it is definitely assigned at the end point of stmt; otherwise, it is not definitely assigned at the end point of stmt.
