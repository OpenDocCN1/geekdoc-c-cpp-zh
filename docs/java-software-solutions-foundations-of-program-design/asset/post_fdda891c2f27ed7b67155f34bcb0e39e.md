
# LISTING 7.4 continued

```
//------------------------------------------------------------------
// Adds this rational number to the one passed as a parameter.
// A common denominator is found by multiplying the individual
// denominators.
//------------------------------------------------------------------
public RationalNumber add (RationalNumber op2)
{
    int commonDenominator = denominator * op2.getDenominator();
    int numerator1 = numerator * op2.getDenominator();
    int numerator2 = op2.getNumerator() * denominator;
    int sum = numerator1 + numerator2;

    return new RationalNumber (sum, commonDenominator);
}

//------------------------------------------------------------------
// Subtracts the rational number passed as a parameter from this
// rational number.
//------------------------------------------------------------------
public RationalNumber subtract (RationalNumber op2)
{
    int commonDenominator = denominator * op2.getDenominator();
    int numerator1 = numerator * op2.getDenominator();
    int numerator2 = op2.getNumerator() * denominator;
    int difference = numerator1 - numerator2;

    return new RationalNumber (difference, commonDenominator);
}

//------------------------------------------------------------------
// Multiplies this rational number by the one passed as a
// parameter.
//------------------------------------------------------------------
public RationalNumber multiply (RationalNumber op2)
{
    int numer = numerator * op2.getNumerator();
    int denom = denominator * op2.getDenominator();

    return new RationalNumber (numer, denom);
}

//------------------------------------------------------------------
// Divides this rational number by the one passed as a parameter
// by multiplying by the reciprocal of the second rational.
//------------------------------------------------------------------
public RationalNumber divide (RationalNumber op2)
{
    return multiply (op2.reciprocal());
}

//------------------------------------------------------------------------------
// Determines if this rational number is equal to the one passed
// as a parameter. Assumes they are both reduced.
//------------------------------------------------------------------------------
public boolean isLike (RationalNumber op2)
{
    return ( numerator == op2.getNumerator() &&
            denominator == op2.getDenominator() );
}

//------------------------------------------------------------------------------
// Returns this rational number as a string.
//------------------------------------------------------------------------------
public String toString ()
{
    String result;
    if (numerator == 0)
        result = "0";
    else
        if (denominator == 1)
            result = numerator + "";
        else
            result = numerator + "/" + denominator;
    return result;
}

//------------------------------------------------------------------------------
// Reduces this rational number by dividing both the numerator
// and the denominator by their greatest common divisor.
//------------------------------------------------------------------------------
private void reduce ()
{
    if (numerator != 0)
    {
        int common = gcd (Math.abs(numerator), denominator);

        numerator = numerator / common;
        denominator = denominator / common;
    }
}

In the software world, we define an aggregate object as any object that contains references to other objects as instance data. For example, an Account object contains, among other things, a String object that represents the name of the account owner. We sometimes forget that strings are objects, but technically that makes each Account object an aggregate object.

Aggregation is a special type of dependency. That is, a class that is defined in part by another class is dependent on that class. The methods of the aggregate object generally invoke the methods of the objects from which it is composed.

Let’s consider another example. The program StudentBody shown in Listing 7.5 creates two Student objects. Each Student object is composed, in part, of two Address objects, one for the student’s address at school and another for the student’s home address. The main method does nothing more than create the Student objects and print them out. Once again we are passing objects to the println method, relying on the automatic call to the toString method to create a valid representation of the object that is suitable for printing.

The Student class shown in Listing 7.6 represents a single student. This class would have to be greatly expanded if it were to represent all aspects of a student. We deliberately keep it simple for now so that the object aggregation is clearly shown. The instance data of the Student class includes two references to Address objects. We refer to those objects in the toString method as we create a string representation of the student. By concatenating an Address object to another string, the toString method in Address is automatically invoked.

## LISTING 7.5

```java
//**********************
// StudentBody.java Author: Lewis/Loftus
//************************
// Demonstrates the use of an aggregate class.
//************************
public class StudentBody
{
// Creates some Address and Student objects and prints them.
//-------------------------
public static void main (String[] args)
{
Address school = new Address ("800 Lancaster Ave.", "Villanova", "PA", 19085);
Address jHome = new Address ("21 Jump Street", "Lynchburg", "VA", 24551);

Student john = new Student ("John", "Smith", jHome, school);

Address mHome = new Address ("123 Main Street", "Euclid", "OH", 44132);
Student marsha = new Student ("Marsha", "Jones", mHome, school);

System.out.println (john);
System.out.println ();
System.out.println (marsha);
}
}
```

## OUTPUT

John Smith
Home Address:
21 Jump Street
Lynchburg, VA 24551
School Address:
800 Lancaster Ave.
Villanova, PA 19085

Marsha Jones
Home Address:
123 Main Street
Euclid, OH 44132
School Address:
800 Lancaster Ave.
Villanova, PA 19085

## LISTING 7.6

```
//************************************************************************
//  Student.java      Author: Lewis/Loftus
//
//  Represents a college student.
//************************************************************************

public class Student
{
    private String firstName, lastName;
    private Address homeAddress, schoolAddress;

//-------------------------------------------------------------------
// Constructor: Sets up this student with the specified values.
//-------------------------------------------------------------------
public Student (String first, String last, Address home,
    Address school)
{
    firstName = first;
    lastName = last;
    homeAddress = home;
    schoolAddress = school;
}

//-------------------------------------------------------------------
// Returns a string description of this Student object.
//-------------------------------------------------------------------
public String toString()
{
    String result;

    result = firstName + " " + lastName + "\n";
    result += "Home Address:\n" + homeAddress + "\n";
    result += "School Address:\n" + schoolAddress;

    return result;
}
}
```

The Address class is shown in Listing 7.7. It represents a street address. Note that nothing about the Address class indicates that it is part of a Student object. The Address class is kept generic by design and therefore could be used in any situation in which a street address is needed.

## LISTING 7.7

```
//*******************************************************************
// Address.java      Author: Lewis/Loftus
//
// Represents a street address.
//*******************************************************************
public class Address
{
private String streetAddress, city, state;
private long zipCode;

//--------------------------------------------------------------------------------
// Constructor: Sets up this address with the specified data.
//--------------------------------------------------------------------------------
public Address (String street, String town, String st, long zip)
{
    streetAddress = street;
    city = town;
    state = st;
    zipCode = zip;
}

//--------------------------------------------------------------------------------
// Returns a description of this Address object.
//--------------------------------------------------------------------------------
public String toString()
{
    String result;

    result = streetAddress + "\n";
    result += city + ", " + state + " " + zipCode;

    return result;
}
}
```

The more complex an object, the more likely it will need to be represented as an aggregate object. In UML, aggregation is represented by a connection between two classes, with an open diamond at the end near the class that is the aggregate. Figure 7.2 shows a UML class diagram for the StudentBody program.

Note that in previous UML diagram examples and in Figure 7.2, strings are not represented as separate classes with aggregation relationships, though technically they could be. Strings are so fundamental to programming that often they are represented as though they were a primitive type in a UML diagram.

## The this Reference

Before we leave the topic of relationships among classes, we should examine another special reference used in Java programs called the this reference. The word this is a reserved word in Java. It allows an object to refer to itself. As we have discussed, a nonstatic method is invoked through (or by) a particular object
