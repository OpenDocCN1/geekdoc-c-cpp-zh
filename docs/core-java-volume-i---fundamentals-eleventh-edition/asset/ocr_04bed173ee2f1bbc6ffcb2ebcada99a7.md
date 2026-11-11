Abstract methods are an important concept in the Java programming language. You will encounter them most commonly inside *interfaces*. For more information about interfaces, turn to Chapter 6.

# Listing 5.4 abstractClasses/PersonTest.java

```
    1 package abstractClasses;
    2
    3 /**
    4  * This program demonstrates abstract classes.
    5  * @version 1.01 2004-02-21
    6  * @author Cay Horstmann
    7  */
    8 public class PersonTest
    9 {
    10    public static void main(String[] args)
    11    {
    12       var people = new Person[2];
    13
    14       // fill the people array with Student and Employee objects
    15       people[0] = new Employee("Harry Hacker", 50000, 1989, 10, 1);
    16       people[1] = new Student("Maria Morris", "computer science");
    17
    18       // print out names and descriptions of all Person objects
    19       for (Person p : people)
    20          System.out.println(p.getName() + ", " + p.getDescription());
    21    }
    22 }
```

# Listing 5.5 abstractClasses/Person.java

```
    1 package abstractClasses;
    2
    3 public abstract class Person
    4 {
    5    public abstract String getDescription();
    6    private String name;
    7
    8    public Person(String name)
    9    {
    10      this.name = name;
    11   }
    12
    13   public String getName()
    14   {
    15      return name;
    16   }
    17 }
```