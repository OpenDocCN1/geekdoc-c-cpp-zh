
When you use inheritance to create the CommissionEmployee class, you acquire the following benefits:

- You save time, because you need not to re-create any fields, properties, or methods already defined in the Employee class.
- You reduce the chance of errors, because the Employee properties and method have already been used and tested.
- You make it easier for anyone who has used the Employee class to understand the CommissionEmployee class because such users can concentrate on the new features only.

The ability to use inheritance makes programs easier to write, understand, and less prone to errors. Imagine that besides CommissionEmployee, you want to create several other specific Employee classes (perhaps PartTimeEmployee, including a property for hours worked, or DismissedEmployee, including a reason for dismissal). You can develop each class correctly and more quickly.

In fact, the concept of class inheritance is useful because it makes class code reusable and development faster. However, do not use inheritance simply to save work. When properly used, inheritance always involves a general-to-specific relationship.

# Understanding Inheritance Terminology

A class that is used as a basis for inheritance, such as Employee, is called a base class. When you create a class that inherits from a base class (such as CommissionEmployee), it is a derived class or extended class. When presented with two classes that have a parent-relationship, you can tell which is the base class and which is the derived class by using the two classes in a sentence with the phrase "is a." A derived class is always "is a" or instance of the more general base class. For example, a Tree class must be a base class to an Evergreen class. Every Evergreen "is a tree", however it is not true that every tree is an Evergreen. Thus, Tree is the base class, and Evergreen is the derived class. Similarly, CommissionEmployee "is an Employee" not always the other around—so Employee is the base class and CommissionEmployee is derived.

You can use the terms superclass and subclass as synonyms for base class and derived class. Thus, Evergreen can be called a subclass of the Tree superclass. You can also use the terms parent class and child class. A CommissionEmployee is a child to the Employee parent. Use the pair of terms with which you are most comfortable; all of these terms will be used interchangeably in this book.

As an alternative to discover which of the classes is the base class and which is the derived class, you can try saying the two class names together (although this technique might not work with every superclass-subclass pair). When people say their names in the English language, they say the more specific name before the all-encompassing name, such as Gimny Kroening. Similarly, with classes, the order "makes more sense" is the child-parent order. Thus, because Evergreen makes more sense than Tree Evergreen, you can deduce that Evergreen is the child class. It is also convenient to think of a derived class as building upon its base class by providing the "adjectives" or additional descriptive terms for the "noun". Frequently, the names of derived classes are formed in this way, as in CommissionEmployee.

Finally, you usually distinguish base classes from their derived classes by size. A derived class is larger than a base class, in the sense that it has additional fields, properties, and methods. A derived class description might look small, but any subclass contains all the fields, properties, and methods of its subclass as well as its own specific ones. Do not think of a subclass as a "subset" of another class—in other words, possessing only parts of its subclass. In fact, a derived class contains everything within the subclass, plus any new attributes and methods.

A derived class can be extended further. In other words, a subclass can have a child of its own. For example, if you create a Tree class and Evergreen, you might derive a Spruce class from Evergreen. a Poodle class might derive from Dog DomesticPet, and DomesticPet from Animal. Similarly, a Poodle class might derive from Dog, Dog from DomesticPet. The entire list of parent classes from which a child class derived constitutes the ancestors of class.

After you create the Spruce class, you might be to create Spruce objects. For example, you might create the TreeInMyBackYard, or you might create an array of 100 Spruce objects for a tree farm. Similarly, one Poodle might be myPetDogFifi.

Inheritance is transitive, which means a class inherits all the members of all its ancestors. In other words, when you declare a Spruce object, it contains all the attributes and methods of both an Evergreen and a Tree. As you work with C#, you will encounter many examples of transitive chains of inheritance.

> When you create your own inheritance chains, you want to place fields and methods at their most general level. In other words, a method named Grow() rightfully belongs in a Tree class, whereas LeavesTurnColor() does not, because the method applies to only some of the Tree classes. Similarly, a LeavesTurnColor() method would be better located in a Deciduous class than separately within the Oak or Maple class.

# CHAPTER 10 Introduction to Inheritance

# TWO TRUTHS & A LIE
Understanding Inheritance

- 1. When you use inheritance to create a class, you save time because you can copy and paste fields, properties, and methods that have already been created for the original class.
- 2. When you use inheritance to create a class, you reduce the chance of errors because the original class's properties and methods have already been used and tested.
- 3. When you use inheritance to create a class, you make it easier for anyone who has used the original class to understand the new class because such users can concentrate on the new features.

> you inherit them.
The original class, you do not copy these class members, already been created for because you you need not re-create fields, properties, and methods that have
The false statement is #1!. When you use inheritance to create a class, you

# Extending Classes

When you create a class that is an extension or child of another class, you use a single colon between the derived class name and its base class name. For example, the following class header creates a subclass-superclass relationship between CommissionEmployee and Employee.

`class CommissionEmployee : Employee`

Each CommissionEmployee object automatically contains all the fields, properties, and methods of the base class; you can then add new components to the new, derived class.
Figure 10-2 shows a CommissionEmployee class.

```c
class CommissionEmployee : Employee {
    public double CommissionRate{get;set;}
}
```

Figure 10-2 The CommissionEmployee class

# Extending Classes

Although you see only one property defined in the CommissionEmployee class in 10-3, it contains three properties: IdNum and Salary, inherited from Employee, and CommissionRate, which is defined within the CommissionEmployee class. Similarly, although you not see any fields or methods in the CommissionEmployee class, it inherits the salary field and meeting of Employee.

Figure 10-3 shows a program with a Main() method that declares Employee and CommissionEmployee objects and shows all the properties and methods that can be used

> Note in the output in Figure 10-4 that these salaries are restricted

Figure 10-3 The DemoEmployees program that declares Employee and CommissionEmployee objects

```
Hello. I am employee #123
Accountant #123 salary: $30,000.00 per year

Hello. I am employee #234
Programmer #234 salary: $15,000.00 per year

Hello. I am employee #345
Salesperson 1 #345 salary: $22,500.00 per year
..plus 7.00 % commission on all sales

Hello. I am employee #456
Salesperson 2 #456 salary: $15,000.00 per year
..plus 4.00 % commission on all sales
```

**Figure 10-4** Output of the DemoEmployees program

Inheritance works only in one direction: A child inherits from a parent–not the other around. If a program instantiates an Employee object as in the following statement, Employee object does not have access to the CommissionEmployee properties or methods.

```csharp
Employee clerk = new Employee();
clerk.CommissionRate = 0.1;
```

> Don't Do It
This statement is invalid–Employee objects do not have a CommissionRate.

Employee is the parent class, and clerk is an object of the parent class. It makes sense that a parent class object not have access to its child's data and methods. When you create the parent class, you do not know how many future classes might be created, or what data or methods might look like. In addition, children are more specific. A HeartSurgeon class and an Obstetrician class are child of a Doctor class. You do not expect all members of the general parent class Doctor to have the HeartSurgeon's RepairValve() method or The Obstetrician's DeliverBaby() method. However, HeartSurgeon and Obstetrician have access to the more general Doctor methods TakeBloodPressure() and BillPatients(). As doctors, it is convenient to think of derived classes as specialists. That is, their fields and methods are more specialized than those of the base class.

Watch the video Inheritance.
