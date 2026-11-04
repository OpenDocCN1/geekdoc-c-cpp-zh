```
public virtual int getAge()
{
    return fAge;
}
public class AdultPerson : Person
{
    public AdultPerson() { }
    override public void setAge(int age)
    {
        if (age > 21)
            base.setAge(age);
    }
}
```

In Listing 4.24, two virtual methods, namely, setAge() and getAge(), are defined inside the class Person. The class AdultPerson inherits the class Person and overrides the method setAge(). The if statement inside the setAge() method of the derived class AdultPerson checks whether the age is greater than 21. If the age is greater than 21, then the setAge() method of the base class Person is called to set the age as per the value passed in the argument. Inside the Main() method of the Program class, the setAge() method from the base class Person and derived class AdultPerson is called.

5 Press the F5 key to run the MethodOverriding application.

The output of the application appears, as shown in Fig.C# 4.22:

![](bbox=[0.35, 0.55, 0.65, 0.68])

Fig.C#4.22

In Fig.C#4.22, you can see that the setAge() method of the base class Person sets the age to 18 and displays it. However, the setAge() method of the derived class AdultPerson does not display the age 18 as it is smaller than 21. Next, let’s discuss how to work with interfaces to implement multiple inheritance.

# Working with Interfaces

Interface is a collection of abstract data members such as methods, events, and properties. Interfaces in C# are introduced to provide the feature of multiple inheritance to classes in C#. The methods defined in an interface do not have their implementation and only specify the parameters they will take and the type of values they will return. An interface is always implemented in a class.

Interface in C# is equivalent to an abstract base class. You cannot instantiate an object through an interface, but you can offer a set of functionalities that is common to several different classes.

Let’s learn how you can define, implement, and inherit an interface in C#.

# Defining an Interface

An interface is declared in a manner similar to that of declaring a class. The difference is that a class is declared with the class keyword and an interface is declared with an interface keyword. The syntax of defining an interface in C# is as follows:

```
interface MyInterface
{
    //Abstract Method Declarations in Interface Body
}
```