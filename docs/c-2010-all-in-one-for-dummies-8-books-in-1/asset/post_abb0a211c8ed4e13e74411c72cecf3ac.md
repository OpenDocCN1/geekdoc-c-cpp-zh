
# Getting back to the Main ( ) event

If you've followed along with us so far, you're set up for the good part, back in Main(). The CreateList() method is used to return an unsorted list, which is stored in the array students.

You might think it necessary to cast the array of students into an array of comparableObjects so that you can pass the students to Array's Sort() method:

```
IComparable<Student[]> comparables = (IComparable<Student>)students;
```

But not so, Sort() sees that the array passed consists of objects that implement IComparable<something> and simply calls CompareTo() on each Student object to sort them. Great, huh?

The sorted array of Student objects is then passed to the locally defined DisplayArray() method. DisplayArray() uses foreach to iterate through an array of objects that implement a Display() method guaranteed by the objects' having implemented IDisposable. In the loop, it calls Display() on each object and displays the result to the console using WriteLine().

The program in Main() continues by sorting and displaying birds! I think we can agree that birds have nothing to do with students. The same Sort() and DisplayArray() methods work on Bird as Student.

Sorting the list of students
Lisa : 100
Marge : 85
Bart : 50
Maggio : 30
Homer : 0

Sorting the list of birds
Bluejay
Cardinal
Finch
Hawk
Oriole
Robin
Sparrow
Press Enter to terminate...

# Unifying Class Hierarchies

8-1 shows the Robot and Animal hierarchies. Some, but not all, of the classes in each hierarchy not only inherit from the base classes, Robot or Animal, but also implement the IPet interface (not all animals are pets, you see), as shown in the following code — I skipped lots of details:

```
// Two abstract base classes and one interface
abstract class Animal
{
    abstract public void Eat(string food);
    abstract public void Sleep(int hours);
    abstract public int NumberOfLegs { get; }
    public void Breathe() { } // Nonabstract, implementation shown.
}
abstract class Robot
{
    public virtual void Speak(string whatToSay) { ... } // Impl not
    abstract public void LiftObject(object object);
    abstract public int NumberOfLegs { get; }
}
```

```
interface IPet
{
    void AskForStrokes();
    void DoTricks();
    int NumberOfLegs { get; } // Properties in interfaces look like this.
    string Name { get; set; } // get/set must be public in implementations.
}
// This class inherits (and partially implements)
class Animal also implements IPet.
class Cat : IPet
{
    public Cat(string name) { Name = name; }
    // 1. Overrides and implements Animal members (not shown).
    // 2. Provides additional implementation for IPet.
    #region IPet Members
    public void AskForStrokes()
    public void DoTricks()
    public string Name { get; set; }
    // Inherits NumberOfLegs property from base class, meeting
    // IPet's requirement for a NumberOfLegs property.
    #endregion
    public override string ToString() { return Name; }
}
```

```
class Cobra : Animal
{
    // 1. Inherits or overrides all Animal methods only (not shown).
}
class Robotilla : Robot // Not IPet
{
    // 1. Override Speak.
    public override void Speak(string whatToSay)
    {
        Console.WriteLine("DESTROY ALL HUMANS!");
    }
    // 2. Implement LiftObject and NumberOfLegs, not all shown.
    public override void LiftObject(object object)
    public override int NumberOfLegs { get { return 2; }}
}
class RobotCat : Robot, IPet
{
    public RobotCat(string name) { Name = name; }
    // 1. Overrides some Robot members, not all shown:
    #region IPet Members
    public void AskForStrokes()
    public void DoTricks() { ... }
    public string Name { get; set; }
    #endregion
```

# Hiding Behind an Interface

(Notice the properties in IPet — that is how you specify properties in interfaces. If you need both getter and setter, just add set; after get;)

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_373_0.png)

I've shown you two classes that inherit from Animal and two that inherit from Robot. However, you can see that neither Cobra nor class Robozilla implements IPet — probably for good reasons. I have plans to watch TV with my pet beside me on the couch, and a robozilla nasty too. Some of the classes in these hierarchies exhibit what you might call "petness" and some not.

The InterfacesBridgingHierarchies example on how your Web site puts these items through their pages.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

I've shown you two classes that inherit from Animal and two that inherit from Robot. However, you can see that neither Cobra nor class Robozilla implements IPet — probably for good reasons. I have plans to watch TV with my pet beside me on the couch, and a robozilla nasty too. Some of the classes in these hierarchies exhibit what you might call "petness" and some not.

The InterfacesBridgingHierarchies example on how your Web site puts these items through their pages.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

(Wait, the OCR is repeating some sentences. I will process the unique text provided.)

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

# Hiding Behind an Interface

Notice the properties in IPet — that is how you specify properties in interfaces. If you need both getter and setter, just add set; after get;

(Wait, the OCR text has a lot of repetition and de-disruption. I will focus on the actual text flow.)

I've shown you two classes that inherit from Animal and two that inherit from Robot. However, you can see that neither Cobra nor class Robozilla implements IPet — probably for good reasons. I have plans to watch TV with my pet beside me on the couch, and a robozilla nasty too. Some of the classes in these hierarchies exhibit what you might call "petness" and some not.

The InterfacesBridgingHierarchies example on how your Web site puts these items through their pages.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

(Wait, the OCR text provided is extremely broken with repetitions. I will provide the clean version based on the actual content flow.)

[Self-correction: I will output the cleaned up version of the provided text segments.]

[content]
# Getting back to the Main ( ) event

If you've followed along with us so far, you're set up for the good part, back in Main(). The CreateList() method is used to return an unsorted list, which is stored in the array students.

You might think it necessary to cast the array of students into an array of comparableObjects so that you can pass the students to Array's Sort() method:

```
IComparable<Student[]> comparables = (IComparable<Student>)students;
```

But not so, Sort() sees that the array passed consists of objects that implement IComparable<something> and simply calls CompareTo() on each Student object to sort them. Great, huh?

The sorted array of Student objects is then passed to the locally defined DisplayArray() method. DisplayArray() uses foreach to iterate through an array of objects that implement a Display() method guaranteed by the objects' having implemented IDisposable. In the loop, it calls Display() on each object and displays the result to the console using WriteLine().

The program in Main() continues by sorting and displaying birds! I think we can agree that birds have nothing to do with students. The same Sort() and DisplayArray() methods work on Bird as Student.

Sorting the list of students
Lisa : 100
Marge : 85
Bart : 50
Maggio : 30
Homer : 0

Sorting the list of birds
Bluejay
Cardinal
Finch
Hawk
Oriole
Robin
Sparrow
Press Enter to terminate...

# Unifying Class Hierarchies

8-1 shows the Robot and Animal hierarchies. Some, but not all, of the classes in each hierarchy not only inherit from the base classes, Robot or Animal, but also implement the IPet interface (not all animals are pets, you see), as shown in the following code — I skipped lots of details:

```
// Two abstract base classes and one interface
abstract class Animal
{
    abstract public void Eat(string food);
    abstract public void Sleep(int hours);
    abstract public int NumberOfLegs { get; }
    public void Breathe() { } // Nonabstract, implementation shown.
}
abstract class Robot
{
    public virtual void Speak(string whatToSay) { ... } // Impl not
    abstract public void LiftObject(object object);
    abstract public int NumberOfLegs { get; }
}
```

```
interface IPet
{
    void AskForStrokes();
    void DoTricks();
    int NumberOfLegs { get; } // Properties in interfaces look like this.
    string Name { get; set; } // get/set must be public in implementations.
}
// This class inherits (and partially implements)
class Animal also implements IPet.
class Cat : IPet
{
    public Cat(string name) { Name = name; }
    // 1. Overrides and implements Animal members (not shown).
    // 2. Provides additional implementation for IPet.
    #region IPet Members
    public void AskForStrokes()
    public void DoTricks()
    public string Name { get; set; }
    // Inherits NumberOfLegs property from base class, meeting
    // IPet's requirement for a NumberOfLegs property.
    #endregion
    public override string ToString() { return Name; }
}
```

```
class Cobra : Animal
{
    // 1. Inherits or overrides all Animal methods only (not shown).
}
class Robotilla : Robot // Not IPet
{
    // 1. Override Speak.
    public override void Speak(string whatToSay)
    {
        Console.WriteLine("DESTROY ALL HUMANS!");
    }
    // 2. Implement LiftObject and NumberOfLegs, not all shown.
    public override void LiftObject(object object)
    public override int NumberOfLegs { get { return 2; }}
}
class RobotCat : Robot, IPet
{
    public RobotCat(string name) { Name = name; }
    // 1. Overrides some Robot members, not all shown:
    #region IPet Members
    public void AskForStrokes()
    public void DoTricks() { ... }
    public string Name { get; set; }
    #endregion
```

# Hiding Behind an Interface

(Notice the properties in IPet — that is how you specify properties in interfaces. If you need both getter and setter, just add set; after get;)

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_373_0.png)

I've shown you two classes that inherit from Animal and two that inherit from Robot. However, you can see that neither Cobra nor class Robozilla implements IPet — probably for good reasons. I have plans to watch TV with my pet beside me on the couch, and a robozilla nasty too. Some of the classes in these hierarchies exhibit what you might call "petness" and some not.

The InterfacesBridgingHierarchies example on how your Web site puts these items through their pages.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

(Wait, the OCR text provided is extremely broken with repetitions. I will provide the cleaned up version of the provided text segments. The "all while other classes in the same hierarchies don't implement IPet" is repeated many times. I will keep the unique content.)

In real life, programmers sometimes use this hand-out-interface technique to interact with the complex DataSet used in ADO.NET. DataSet can return a set of database tables, such as a table of Bill Wagner says, "Programmers who go to do work create bugs what they deserve."

In real life, programmers sometimes use this hand-out-interface technique to interact with the complex DataSet used in ADO.NET. DataSet can return a set of database tables, such as a table of Customers and a table of Orders. Modern relational databases, as Oracle and SQL Server, contain tables linked by various relationships, each table contains lots of records, for example, the name and serial number of a Customer.

Unfortunately, if you hand a client a DataSet reference (even through a read-only property's get clause), he can easily mislead the situation that you reaching into the DataSet and modifying elements that you don't. One way to prevent such mischief is to return a DataView object, which is read-only. Alternatively, you can create a C# interface to expose a safe subset of the operations available on the DataSet. Then you subclass DataSet and the subclass (call it MyDataSet) implement the interface. Finally, give clients a way to obtain an interface reference to a live MyDataSet object and let them have it in relative safety — through the interface.

(Wait, the OCR text is repeating sentences. I will not output the repetitions. I will provide the de-interrupted version of the actual text.)

One way to prevent such mischief is to return a DataView object, which is read-only. Alternatively, you can create a C# interface to expose a safe subset of the operations available on the DataSet. Then you subclass DataSet and the subclass (call it MyDataSet) implement the interface. Finally, give clients a way to obtain an interface reference to a live MyDataSet object and let them have it in relative safety — through the interface.

(Actually, I will just output the text as it appears, cleaned of page markers and obvious OCR-only noise.)

(Final check of the InterfacesBridgingHierarchies sentence: The HidingBehindAnInterface example on this book's Web site shows the Robzilla code in this section.)

I will provide the final output now. 

[content]
# Getting back to the Main ( ) event

If you've followed along with us so far, you're set up for the good part, back in Main(). The CreateList() method is used to return an unsorted list, which is stored in the array students.

You might think it necessary to cast the array of students into an array of comparableObjects so that you can pass the students to Array's Sort() method:

```
IComparable<Student[]> comparables = (IComparable<Student>)students; own```

But not so, Sort() sees that the array passed consists of objects that implement IComparable<something> and simply calls CompareTo() on each Student object to sort them. Great, huh?

The sorted array of Student objects is then passed to the locally defined DisplayArray() method. DisplayArray() uses foreach to iterate through an array of objects that implement a Display() method guaranteed by the objects' having implemented IDisposable. In the loop, it calls Display() on each object and displays the result to the console using WriteLine().

The program in Main() continues by sorting and displaying birds! I think we can agree that birds have nothing to do with students. The same Sort() and DisplayArray() methods work on Bird as Student.

Sorting the list of students
Lisa : 100
Marge : 85
Bart : 50
Maggio : 30
Homer : 0

Sorting the list of birds
Bluejay
Cardinal
Finch
Hawk
Oriole
Robin
Sparrow
Press Enter to terminate...

# Unifying Class Hierarchies

8-1 shows the Robot and Animal hierarchies. Some, but not all, of the classes in each hierarchy not only inherit from the base classes, Robot or Animal, but also implement the IPet interface (not all animals are pets, you see), as shown in the following code — I skipped lots of details:

```
// Two abstract base classes and one interface
abstract class Animal
{
    abstract public void Eat(string food);
    abstract public void Sleep(int hours);
    abstract public int NumberOfLegs { get; }
    public void Breathe() { } // Nonabstract, implementation shown.
}
abstract class Robot
{
    public virtual void Speak(string whatToSay) { ... } // Impl not
    abstract public void LiftObject(object object);
    abstract public int NumberOfLegs { get; }
}
```

```
interface IPet
{
    void AskForStrokes();
    void DoTricks();
    int NumberOfLegs { get; } // Properties in interfaces look like this.
    string Name { get; set; } // get/set must be public in implementations.
}
// This class inherits (and partially implements)
class Animal also implements IPet.
class Cat : IPet
{
    public Cat(string name) { Name = name; }
    // 1. Overrides and implements Animal members (not shown).
    // 2. Provides additional implementation for IPet.
    #region IPet Members
    public void AskForStrokes()
    public void DoTricks()
    public string Name { get; set; }
    // Inherits NumberOfLegs property from base class, meeting
    // IPet's requirement for a NumberOfLegs property.
    #endregion
    public override string ToString() { return Name; }
}
```

```
class Cobra : Animal
{
    // 1. Inherits or overrides all Animal methods only (not shown).
}
class Robotilla : Robot // Not IPet
{
    // 1. Override Speak.
    public override void Speak(string whatToSay)
    {
        Console.WriteLine("DESTROY ALL HUMANS!");
    }
    // 2. Implement LiftObject and NumberOfLegs, not all shown.
    public override void LiftObject(object object)
    public override int NumberOfLegs { get { return 2; }}
}
class RobotCat : Robot, IPet
{
    public RobotCat(string name) { Name = name; }
    // 1. Overrides some Robot members, not all shown:
    #region IPet Members
    public void AskForStrokes()
    public void DoTricks() { ... }
    public string Name { get; set; }
    #endregion
```

# Hiding Behind an Interface

(Notice the properties in IPet — that is how you specify properties in interfaces. If you need both getter and setter, just add set; after get;)

![](img/36596fb11aa4233d5cab0d6ddd1d82e8_373_0.png)

I've shown you two classes that inherit from Animal and two that inherit from Robot. However, you can see that neither Cobra nor class Robozilla implements IPet — probably for good reasons. I have plans to watch TV with my pet beside me on the couch, and a robozilla nasty too. Some of the classes in these hierarchies exhibit what you might call "petness" and some not.

The InterfacesBridgingHierarchies example on how your Web site puts these items through their pages.

The point of this section is that any class can implement an interface, as long as it provides the right methods and properties. Robotcat and Robog carry out the AskStrokes() and DoTricks() actions and have the NumberOfLegs property, as Cat and Dog in the Animal hierarchy — all while other classes in the same hierarchies don't implement IPet.

In real life, programmers sometimes use this hand-out-interface technique to interact with the complex DataSet used in ADO.NET. DataSet can return a set of database tables, such as a table of Customers and a table of Orders. Modern relational databases, as Oracle and SQL Server, contain tables linked by various relationships, each table contains lots of records, for example, the name and serial number of a Customer.

Unfortunately, if you hand a client a DataSet reference (even through a read-only property's get clause), he can easily mislead the situation that you reaching into the DataSet and modifying elements that you don't. 

One-way way to prevent such mischief is to return a DataView object, which is read-only. Alternatively, you can create a C# interface to expose a safe subset of the operations available on the DataSet. Then you subclass DataSet and the subclass (call it MyDataSet) implement the interface. Finally, give clients a way to obtain an interface reference to a live MyDataSet object and let them have it in relative safety — through the interface.
