
## 5.1 Classes, Superclasses, and Subclasses

Let’s return to the Employee class discussed in the previous chapter. Suppose (alas) you work for a company where managers are treated differently from other employees. Managers are, of course, just like employees in many respects. Both employees and managers are paid a salary. However, while employees are expected to complete their assigned tasks in return for receiving their salary, managers get bonuses if they actually achieve what they are supposed to do. This is the kind of situation that cries out for inheritance. Why? Well, you need to define a new class, Manager, and add functionality. But you can retain some of what you have already programmed in the Employee class, and all of the fields of the original class can be preserved. More abstractly, there is an obvious “is–a” relationship between Manager and Employee. Every manager is an employee: This “is–a” relationship is the hallmark of inheritance.

> **NOTE:**
>
> In this chapter, I use the classic example of employees and managers, but I must ask you to take this example with a grain of salt. In the real world, an employee can become a manager, so you would want to model being a manager as a role of an employee, not a subclass. In my example, however, I assume the corporate world is populated by two kinds of people: those who are forever employees, and those who have always been managers.

### 5.1.1 Defining Subclasses

Here is how you define a Manager class that inherits from the Employee class. Use the Java keyword extends to denote inheritance.

```java
public class Manager extends Employee
{
    added methods and fields
}
```

> **C++ NOTE:**
>
> Inheritance is similar in Java and C++. Java uses the `extends` keyword instead of the `:` token. All inheritance in Java is public inheritance; there is no analog to the C++ features of private and protected inheritance.

The keyword `extends` indicates that you are making a new class that derives from an existing class. The existing class is called the *superclass*, *base class*, or *parent class*. The new class is called the *subclass*, *derived class*, or *child class*. The terms superclass and subclass are those most commonly used by Java programmers, although some programmers prefer the parent/child analogy, which also ties in nicely with the “inheritance” theme.

The `Employee` class is a superclass, but not because it is superior to its subclass or contains more functionality. *In fact, the opposite is true:* Subclasses have *more* functionality than their superclasses. For example, as you will see when we go over the rest of the `Manager` class code, the `Manager` class encapsulates more data and has more functionality than its superclass `Employee`.

> **NOTE:**
>
> The prefixes *super* and *sub* come from the language of sets used in theoretical computer science and mathematics. The set of all employees contains the set of all managers, and thus is said to be a *superset* of the set of managers. Or, to put it another way, the set of all managers is a *subset* of the set of all employees.

Our `Manager` class has a new field to store the bonus, and a new method to set it:

```java
public class Manager extends Employee
{
   private double bonus;
   . . .
   public void setBonus(double bonus)
   {
      this.bonus = bonus;
   }
}
```

There is nothing special about these methods and fields. If you have a `Manager` object, you can simply apply the `setBonus` method.

```java
Manager boss = . . .;
boss.setBonus(5000);
```

Of course, if you have an `Employee` object, you cannot apply the `setBonus` method—it is not among the methods defined in the `Employee` class.

However, you *can* use methods such as `getName` and `getHireDay` with `Manager` objects. Even though these methods are not explicitly defined in the `Manager` class, they are automatically inherited from the `Employee` superclass.

Every `Manager` object has four fields: name, salary, hireDay, and bonus. The fields name, salary, and hireDay are taken from the superclass.

> **NOTE:**
>
> The Java language specification states: “Members of a class that are declared private are not inherited by subclasses of that class.” This has confused my readers over the years. The specification uses the word “inherits” narrowly. It considers the private fields non-inherited because the `Manager` class cannot access them directly. Thus, every `Manager` object has three fields from the superclass, but the `Manager` class does not “inherit” them.

When defining a subclass by extending its superclass, you only need to indicate the *differences* between the subclass and the superclass. When designing classes, you place the most general methods in the superclass and more specialized methods in its subclasses. Factoring out common functionality by moving it to a superclass is routine in object-oriented programming.

> **NOTE:**
>
> In chapter 4, you learned about *records*: classes whose state is entirely defined by the constructor parameters. You cannot extend a record, and a record cannot extend another class.

### 5.1.2 Overriding Methods

Some of the superclass methods are not appropriate for the `Manager` subclass. In particular, the `getSalary` method should return the sum of the base salary and the bonus. You need to supply a new method to *override* the superclass method:

```java
public class Manager extends Employee
{
   . . .
   public double getSalary()
   {
      . . .
   }
   . . .
}
```

How can you implement this method? At first glance, it appears to be simple — just return the sum of the `salary` and `bonus` fields:

```java
public double getSalary()
{
    return salary + bonus; // won't work
}
```

However, that won’t work. Recall that only the `Employee` methods have direct access to the private fields of the Employee class. This means that the `getSalary` method of the Manager class cannot directly access the salary field. If the Manager methods want to access those private fields, they have to do what every other method does—use the public interface, in this case the public `getSalary` method of the `Employee` class.

So, let’s try again. You need to call `getSalary` instead of simply accessing the salary field:

```java
public double getSalary()
{
    double baseSalary = getSalary(); // still won't work
    return baseSalary + bonus;
}
```

Now, the problem is that the call to `getSalary` simply calls *itself*, because the Manager class has a `getSalary` method (namely, the method we are trying to implement). The consequence is an infinite chain of calls to the same method, leading to a program crash.

We need to indicate that we want to call the `getSalary` method of the `Employee` superclass, not the current class. Use the special keyword `super` for this purpose. The call

```java
super.getSalary()
```

calls the `getSalary` method of the `Employee` class. Here is the correct version of the `getSalary` method for the Manager class:

```java
public double getSalary()
{
    double baseSalary = super.getSalary();
    return baseSalary + bonus;
}
```

> **NOTE:**
>
> Some people think of `super` as being analogous to the `this` reference. However, that analogy is not quite accurate: `super` is not a reference to an object. For example, you cannot assign the value `super` to another object variable. Instead, `super` is a special keyword that directs the compiler to invoke the superclass method.

As you saw, a subclass can *add* fields, and it can *add* methods or *override* the methods of the superclass. However, inheritance can never take away any fields or methods.

> **C++ NOTE:**
>
> Java uses the keyword `super` to call a superclass method. In C++, you would use the name of the superclass with the `::` operator instead. For example, the `getSalary` method of the `Manager` class would call `Employee::getSalary` instead of `super.getSalary`.

### 5.1.3 Subclass Constructors

To complete our example, let us supply a constructor.

```java
public Manager(String name, double salary, int year, int month,
               int day)
```
