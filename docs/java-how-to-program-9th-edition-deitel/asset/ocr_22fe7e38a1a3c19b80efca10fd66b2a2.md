EmployeeTest method main (Fig. 8.13) instantiates two Employee objects (lines 13–14). When each Employee object’s constructor is invoked, lines 15–16 of Fig. 8.12 assign the Employee’s first name and last name to instance variables firstName and lastName. These two statements do not make copies of the original String arguments. Actually, String objects in Java are immutable—they cannot be modified after they’re created. Therefore, it’s safe to have many references to one String object. This is not normally the case for objects of most other classes in Java. If String objects are immutable, you might wonder why we’re able to use operators + and += to concatenate String objects. String concatenation operations actually result in a new Strings object containing the concatenated values. The original String objects are not modified.

When main has finished using the two Employee objects, the references e1 and e2 are set to null at lines 31–32. At this point, references e1 and e2 no longer refer to the objects that were instantiated in lines 13–14. The objects become “eligible for garbage collection” because there are no more references to them in the program.

```
// Fig. 8.13: EmployeeTest.java
// static member demonstration.

public class EmployeeTest
{
    public static void main( String[] args )
    {
        // show that count is 0 before creating Employees
        System.out.printf( "Employees before instantiation: %d\n",
            Employee.getCount() );

        // create two Employees; count should be 2
        Employee e1 = new Employee( "Susan", "Baker" );
        Employee e2 = new Employee( "Bob", "Blue" );

        // show that count is 2 after creating two Employees
        System.out.println( "\nEmployees after instantiation: " );
        System.out.printf( "via e1.getCount(): %d\n", e1.getCount() );
        System.out.printf( "via e2.getCount(): %d\n", e2.getCount() );
        System.out.printf( "via Employee.getCount(): %d\n",
            Employee.getCount() );

        // get names of Employees
        System.out.printf( "\nEmployee 1: %s %s\nEmployee 2: %s %s\n",
            e1.getFirstName(), e1.getLastName(),
            e2.getFirstName(), e2.getLastName() );

        // in this example, there is only one reference to each Employee,
        // so the following two statements indicate that these objects
        // are eligible for garbage collection
        e1 = null;
        e2 = null;
    } // end main
} // end class EmployeeTest
```