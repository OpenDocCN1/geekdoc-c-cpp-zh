
## Methods

- Use Pascal case to name methods.
- Use verbs or verb phrases as part of the name to tell what the method does. Avoid writing long methods. Each method should focus on a single theme. Typically, methods should not have more than 25 lines of code.

## Constructor Guidelines

- Constructors use the same identifier as the class.
- Use a consistent ordering for constructors. A common practice is to list constructor methods with the fewest parameters first and the most parameters last. This enables you to provide more details as parameters are added.
- Provide a default constructor if you define even one other constructor.
- Minimize the amount of work done in the constructor. Constructors should not do more than capture the constructor parameter or parameters.

## Spacing Conventions

- Use tabs instead of spaces for indentation.
- Use white space (one blank line) to separate and organize logical groups of code within methods. There should be one and only one single blank line between each method inside the class.
- Use white space (one blank line) to separate properties and instance methods.
- Place curly braces { } at the same level as the method name, but on a new line.
- Avoid writing long instance methods.

## RESOURCES

Additional sites you might want to explore:

- C# Coding Standards and Best Practices at  
  http://www.dotnetspider.com/tutorials/BestPractices.aspx
- C# Station Tutorial - Introduction to Classes at  
  http://www.csharp-station.com/Tutorials/Lesson07.aspx
- Softsteel Solutions Tutorials at  
  http://www.softsteel.co.uk/tutorials/cSharp/contents.html
- Introduction to Objects and Classes in C# at  
  http://www.devarticles.com/c/a/C-Sharp/Introduction-to-Objects-and-Classes-in-C-sharp/

## QUICK REVIEW

- 1. Instance methods require that an `object` be instantiated before they can be accessed.
- 2. Private members are accessible only within the body of the `class` in which they are declared.
- 3. Often in object-oriented development, data is defined with a `private` modifier, and methods that access the data are declared to have `public` access.
- 4. Methods are the members of a `class` that describe the behavior of the data.
- 5. Many programmers employ the standard convention of using an action verb phrase to name methods.
- 6. Overloaded methods are methods with the same name but a different number, type, or arrangement of parameters. For example, the `doSomething()` method is overloaded with the following headings: `public void doSomething(int x, string y)` and `public void doSomething(string y, int x)`.
- 7. Constructors are special methods that create instances of a `class`. Constructors do not return a value—not even `void`.
- 8. Constructors use the same identifier as the `class` name. The keyword `new` is used to call the constructors.
- 9. When you design a class, you normally use `public` access modifiers with constructors and most other methods and `private` access modifier for data members.
- 10. The default constructor has an empty body and it is automatically created if you do not write one. If you write even one constructor, you lose the default constructor and have to write it.
- 11. Accessors are methods that are used to access a `private` data members. Accessors are also referred to as getter methods.
- 12. Mutators are methods that are used to change the current state of `object` members’ data. Mutator methods are also referred to as setters.
- 13. A property looks like a data field and provides a way to set or get `private` member data. You can define the set without the get or vice versa. It is not necessary to include both.
- 14. To call non-value-returning methods, simply type the method’s name. If it is a `static` method, qualify it with the `class` name. If it is an instance method, qualify the identifier with an `object`. If the method has parameters, the call includes actual arguments inside the parentheses, without the types.

## EXERCISES

- 1. Objects are instances of __________.
  - a. data members
  - b. parameters
  - c. properties
  - d. methods
  - e. classes

- 2. Properties are defined with ________ access mode.
  - a. `public`
  - b. `static`
  - c. `private`
  - d. `void`
  - e. `protected`

- 3. Which of the following modifiers is the most restrictive?
  - a. `private`
  - b. `static`
  - c. `public`
  - d. `internal`
  - e. `protected`

- 4. Which of the following identifiers follows the standard naming convention for naming a class?
  - a. Calculate Final Grade
  - b. MilesPerGallon
  - c. Students
  - d. Reports
  - e. Employee

- 5. Which of the following would be the most appropriate way to invoke the `CalculateAvg( )` method found in the Student **class** if an object named `gradStudent` had been instantiated from the class?

  `public static double CalculateAvg(double, double)`

  - a. `gradStudent = CalculateAvg(87.2, 90);`
  - b. `answer = Student.CalculateAvg(87.2, 90);`
  - c. `CalculateAvg(87.2, 90);`
  - d. `answer = gradStudent.CalculateAvg(double, double);`
  - e. `answer = gradStudent.CalculateAvg(87.2, 90);`

- 6. Which of the following is one of the methods inherited from the `object class`?
  - a. `ToString( )`
  - b. `Main( )`
  - c. `CalculateAvg( )`
  - d. `EqualsHashCode( )`
  - e. `TypeHashCode( )`

- 7. Properties are associated with the ______ of the class while methods are affiliated with the ______ of the class.
  - a. `activity` `fields`
  - b. `accessors` `mutators`
  - c. `objects` `instances`
  - d. `data` `behavior`
  - e. `behavior` `data`

- 8. Which of the following is a valid overloaded method for CalculateAvg( )?

  `int CalculateAvg(int val1, int val2)`

  - a. `void CalculateAvg(int val1, int val2)`
  - b. `int CalculateAvg(int val1, int val2)`
  - c. `int CalculateAvg(double val1, double val2)`
  - d. `double CalculateAvg(int val1, int val2)`
  - e. `int CalculateAverage(int val2, int val1)`

- 9. What operator is used to instantiate the class?
  - a. method
  - b. plus symbol
  - c. `ToString( )`
  - d. `new`
  - e. equal symbol

- 10. Instance variables are the same as:
  - a. `private` member data
  - b. local variables
  - c. properties
  - d. arguments
  - e. parameters

- 11. Given the Employee class shown below, which of the following would be the most appropriate heading for its default constructor?

  ```
  public class Employee {
  ```

  - a. `public void Employee( )`
  - b. `public Employee( )`
  - c. `public static Employee( )`
  - d. `private void Employee( )`
  - e. `private Employee( )`

- 12. The following is probably an example of a _____________.

  ```
  public double GetYards( )
  ```

  - a. constructor
  - b. mutator
  - c. property
  - d. accessor
  - e. class definition

- 13. If you follow the standard C# naming conventions, the property name for the following instance variable would be:

  ```
  private string name;
  ```

  - a. propertyName
  - b. nameProperty
  - c. getName
  - d. name
  - e. Name

- 14. Which of the following would be a valid call to the default constructor for the following class?

  ```
  public class Employee {
  ```

  - a. Employee employee1 = new Employee( );
  - b. Employee employee1 = new undergrad( );
  - c. Employee employee1;
  - d. Employee employee1 = new Employee(default);
  - e. Not enough information is given to be able to answer.

- 15. Given the following class definition, what would be a valid heading for a mutator?

  ```
  public class Student {
      private string name;
      private double gpa;
  }
  ```

  - a. `public double SetGpa(double gpaValue)`
  - b. `public void SetGpa(double gpaValue)`
  - c. `public double SetGpa( )`
  - d. `public void GetGpa(double gpaValue)`
  - e. `public double SetGpa( )`

- 16. With a UML class diagram
  - a. the name of the class appears at the bottom section of the diagram
  - b. data members show a + to indicate public access
  - c. methods are not shown
  - d. objects of the class appear in the middle section of the diagram
  - e. methods show the return type on the diagram

- 17. Which of the following modifiers in C# is used with constructors?
  - a. `const`
  - b. `private`
  - c. `public`
  - d. `static`
  - e. `protected`

- 18. Normally, member data uses a __________ access modifier, and methods use a __________ access modifier for object-oriented solutions.
  - a. `protected` `public`
  - b. `private` `protected`
  - c. `public` `protected`
  - d. `public` `private`
  - e. `private` `public`

- 19. For a class called Account that has data members of accountNumber, balance, and transactionAmount, which would be the most appropriate instance method heading for a method that reduces the transaction amount from the current balance?
  - a. `static double ReduceAccount(double accountBalance, double transactionAmount)`
  - b. `double ReduceAccount(double accountBalance, double transactionAmount)`
  - c. `static ReduceAccount( )`
  - d. `void ReduceAccount( )`
  - e. `static void ReduceAccount( )`
