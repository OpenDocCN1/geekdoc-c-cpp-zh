# Use structures to clarify data relationships

Structures bundle groups of related items together. Sometimes the hardest part of figuring out a program is figuring out which data goes with which other data. It’s like going to a small town and asking who’s related to whom. You come to find out that everybody’s kind of related to everybody else, but not really, and you never get a good answer.

If the data has been carefully structured, figuring out what goes with what is much easier. Here’s an example of data that hasn’t been structured:

```
Visual Basic Example of Misleading, Unstructured Variables
name = inputName
address = inputAddress
phone = inputPhone
title = inputTitle
department = inputDepartment
bonus = inputBonus
```

Because this data is unstructured, it looks as if all the assignment statements belong together. Actually, name, address, and phone are variables associated with individual employees, and title, department, and bonus are variables associated with a supervisor. The code fragment provides no hint that there are two kinds of data at work. In the code fragment below, the use of structures makes the relationships clearer:

```
Visual Basic Example of More Informative, Structured Variables
employee.name = inputName
employee.address = inputAddress
employee.phone = inputPhone

supervisor.title = inputTitle
supervisor.department = inputDepartment
supervisor.bonus = inputBonus
```

In the code that uses structured variables, it’s clear that some of the data is associated with an employee, other data with a supervisor.

# Use structures to simplify operations on blocks of data

You can combine related elements into a structure and perform operations on the structure. It’s easier to operate on the structure than to perform the same operation on each of the elements. It’s also more reliable, and it takes fewer lines of code.

Suppose you have a group of data items that belong together—for instance, data about an employee in a personnel database. If the data isn’t combined into a structure, merely copying the group of data can involve a lot of statements. Here’s an example in Visual Basic: