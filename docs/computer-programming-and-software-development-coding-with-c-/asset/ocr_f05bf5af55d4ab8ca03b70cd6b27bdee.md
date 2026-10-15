# Chapter 22 Is-A Relation Basics

What inheritance in C# is bringing is what is sometimes referred to as the relation. Indeed, even in the spoken word, we would say a manager is an employee. The relation is exactly what inheritance is bringing us, also in the behavior we're getting in our C# code.

```
Manager m1 = new Manager();//Manager derives from Employee
Researcher r2 = new Researcher();//Researcher derives from Employee
m1.PerformWork(); //will call PerformWork() on the base Employee class
r2.PerformWork(); //will call PerformWork() on the base Employee class
```

When we define a Manager instance where the Manager class derives from Employee, all public or protected members defined on the base Employee class become available for Manager. If PerformWork is a public or protected method on the Employee class, because the manager is an employee, it becomes available for the manager. The Manager class can, like we've seen in a demonstration, add new functionality, which is then only available for Manager instances, not for Employee instances. And multiple types can inherit from the base Employee class. If Researcher 2 inherits from the base Employee class, every Researcher 2 is an Employee, and therefore Researcher instances will get access to PerformWork as well.