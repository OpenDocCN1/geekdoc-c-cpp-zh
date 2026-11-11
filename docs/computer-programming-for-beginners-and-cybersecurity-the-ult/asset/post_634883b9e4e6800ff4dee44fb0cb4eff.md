
- Java’s networking capabilities make it easier for programmers to create software solutions for shared computing environments.
- The close relationship between Java, C++, and C languages makes it easier for anyone with knowledge of the other two languages to learn Java.
- Java’s automated garbage collection provides continuous memory protection, making it convenient for programmers to eliminate security vulnerabilities while writing codes.
- Java’s architecture is flexible for the implementation of multithreading programs.
- Java is readily reusable, thanks to the ability to redeploy classes using the interface or inheritance features.

## The Downsides of Java

- Since Java is not a native application, it runs at lower speeds compared to other programming languages.
- Java may also lack consistency in the processing and displaying of graphics. For example, the ordinary appearance of the graphical user interface (GUI) in Java-based applications is quite different and of lower standards compared to the GUI output of native software applications.
- Java’s garbage collection, a feature that manages memory efficiency, may interfere with speed and performance whenever it runs as a background application.

## CHAPTER 5: Objects and Classes

Finally, we are going to look at classes and objects.

An object in Java has got to have a state, which will be stored in a field and a behavior, indicated by a method. A class is a sort of map, a blueprint if you like, from which an object is created. This is what a class looks like:

```java
public class Dog {
    String breed;

    int age;

    String color;

    void barking() {

    }

    void whining() {

    }

    void sleeping() {

    }
}
```

A class may have any of these variable types:

- Local—defined within a constructor, block, or method. The variable is declared and then initialized inside a method and destroyed once the method has ended.
- Instance—defined in a class but are outside a method. Initialized when instantiation of the class happens and can be accessed from inside any constructor, block, or method of the class.
- Class—declared inside the class, uses the static keyword, and are outside any method.

Classes can have multiple methods, as many as required to access all the different kinds of values in the method. In our example above, we had three methods—barking(), whining(), and sleeping().

### Constructors

Every class will have a constructor; if you omit it, a default one will be built by the compiler. When you create a new object, at least one constructor must be invoked. As a rule, the name of a constructor must be the same as that of the class, and there can be as many constructors as a class requires.

This is what a constructor looks like:

```java
public class Puppy {

    public Puppy() {
    }

    public Puppy(String name) {
        // This constructor has a single parameter, name.
    }
}
```

### Creating Objects

We already know that a class is a kind of blueprint to create objects from, so it goes without saying that the object is created from the class. For a new object to be created, we need the new keyword.

These are the three steps needed to create an object from a class:

- Declaration—A variable must be declared with a name and the object type
- Instantiation—The new keyword is used for creating the object
- Initialization—The constructor is called, and this initializes the object.

The next example shows how objects are created:

```java
public class Puppy {

    public Puppy(String name) {

        // This constructor contains a single parameter called name.

        System.out.println("Passed Name is :" + name );

    }

    public static void main(String []args) {

        // The next statement will create an object called myPuppy

        Puppy myPuppy = new Puppy( "fluffy" );

    }

}
```

Run this and see what happens.

### Accessing Instance Variables and Methods

Objects can be used when we want to access instance variables and methods; this example shows how we access an instance variable:

```java
/* First we create the object */

ObjectReference = new Constructor();

/* Now we call our variable, like this */

ObjectReference.variableName;

/* Now a class method is called, like this */
ObjectReference.MethodName();
```

Next, we can see the instance variables and methods in a class are accessed:

```java
public class Puppy {
    int PuppyAge;

    public Puppy(String name) {
        // This constructor contains a single parameter called name.
        System.out.println("Name chosen is :" + name );
    }

    public void setAge(int age) {
        PuppyAge = age;
    }

    public int getAge() {
        System.out.println("Puppy's age is :" + PuppyAge );
        return PuppyAge;
    }

    public static void main(String[] args) {
        /* Object creation */
        Puppy myPuppy = new Puppy( "fluffy" );

        /* Now we call the class method to set the Puppy's age */
        myPuppy.setAge(2);

        /* Next, we call another class method to get the Puppy's age */
        myPuppy.getAge();

        /* We access instance variable in this way */

        System.out.println("Variable Value :" + myPuppy.PuppyAge );

    }

}
```

Run this and see what happens.

### Import Statements

One important thing to remember is that paths must be fully qualified, and that includes the names of the class and the package. If not, the compiler will struggle to load the source code and the classes. To qualify a path, we need to use import statements and, in this example, we see how a compiler loads the requested classes into the directory we specify:

```java
import java.io.*;
```

Next, we need two classes created, one called Employee and one called EmployeeTest. We use the following code to do this—keep in mind that Employee is the name of the class, and it is a public class. Do this and then save the file, calling it Employee.java.

Also note that we have four instance variables here—age, name, designation, and salary, along with one constructor that has been explicitly defined and that takes a parameter:

```java
public class Employee {

    String name;

    int age;

    String designation;

    double salary;

    // This is the constructor of the class called Employee
    public Employee(String name) {
        this.name = name;
    }

    // We assign the age of the Employee to the variable called age.
    public void empAge(int empAge) {
        age = empAge;
    }

    /* We assign the designation to the variable called designation.*/
    public void empDesignation(String empDesig) {
        designation = empDesig;
    }

    /* We assign the salary to the variable called salary.*/
    public void empSalary(double empSalary) {
        salary = empSalary;
    }

    /* Print the Employee details */
    public void printEmployee() {
        System.out.println("Name:"+ name );
        System.out.println("Age:" + age );
        System.out.println("Designation:" + designation );
        System.out.println("Salary:" + salary);
    }
}
```

Code processing begins with a main method, so you need to ensure that your code has a main method, and we need to create some objects. We will start by creating a class called EmployeeTest, and this will create a couple of instances of the class called Employee. The methods for each object must be invoked so that the values may be assigned to the variables. Save this code in EmployeeTest:

```java
public class EmployeeTest {

    public static void main(String args[]) {

        /* Create two objects by using constructor */

        Employee empOne = new Employee("Bobby Bucket");

        Employee empTwo = new Employee("Shelley Mary");

        // Invoke the methods for each of the objects we created

        empOne.empAge(28);

        empOne.empDesignation("Senior Software Developer");

        empOne.empSalary(1500);

        empOne.printEmployee();

        empTwo.empAge(22);

        empTwo.empDesignation("Software Developer");

        empTwo.empSalary(850);

        empTwo.printEmployee();

    }

}
```

Now the classes need to be compiled, and EmployeeTest run; do this and see what you get.

You should see this:

## CHAPTER 6: Proper Working Code Examples

Traditionally, everyone's first program prints, "Hello World." This first program demonstrates how to create, save, and run a program. It also shows the basic structure used in all Java programs.

Here's a screenshot of the window created by the Hello World program:

![](img/ecb1bfa35f80f656f92811abb43b3df7_130_0.png)
