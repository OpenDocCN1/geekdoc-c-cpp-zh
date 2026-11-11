```
```java
public String getName()
{
    return name;
}

// more methods
. . .
}
```
```

We break down the implementation of this class, in some detail, in the
sections that follow. First, though, Listing 4.2 is a program that shows the
`Employee` class in action.

In the program, we construct an `Employee` array and fill it with three `Employee`
objects:

```
```java
Employee[] staff = new Employee[3];

staff[0] = new Employee("Carl Cracker", . . .);
staff[1] = new Employee("Harry Hacker", . . .);
staff[2] = new Employee("Tony Tester", . . .);
```
```

Next, we use the `raisesalary` method of the `Employee` class to raise each
employee’s salary by 5%:

```
```java
for (Employee e : staff)
    e.raiseSalary(5);
```
```

Finally, we print out information about each employee, by calling the
`getName`, `getSalary`, and `getHireDay` methods:

```
```java
for (Employee e : staff)
    System.out.println("name=" + e.getName()
        + ",salary=" + e.getSalary()
        + ",hireDay=" + e.getHireDay());
```
```