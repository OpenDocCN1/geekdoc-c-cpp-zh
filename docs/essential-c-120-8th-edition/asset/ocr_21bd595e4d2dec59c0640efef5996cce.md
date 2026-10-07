7.20 demonstrates this by first checking whether entity is a Person and then casting Entity to a Person:

```
// ...
if (entity is Person)
{
    Person person = (Person) entity;
// ...
```

The advantage is that the operator enables a code path for when the explicit cast might fail without the expense of exception handling. With the addition of declaration in C# 7.0 and later, the is operator (and switch syntax shown next) will make the type check and the assignment in the same step. Listing 7.20 demonstrates this with the is Employee code snippet:

```
if (entity is Employee employee)
{
// ...
```

Here, in checking whether the input operand is an employee, it also declares a new variable of type Employee. The result from GetObjectById(id), therefore, is checked against the Employee type—type pattern matching—and assigned to the variable employee in the same expression. If the result of GetObjectById(id) is null or not an Employee, then false is produced, and the else clause executes.

Note that the employee variable is available within and after the if statement; however, it would need to be assigned a value before accessing it inside or after the else clause. Also, you can implicitly specify the data type with var, as expected, but with local variable declaration in general, use caution when the data type't obvious.

# Type Checking with switch Statements

The switch statement also allows for type checking, but it can check for multiple types in addition to null checking—all within the same statement. In Listing 7.21, we demonstrate this with a method that returns the time (using .NET 6.0's TimeOnly), from a variety of types.