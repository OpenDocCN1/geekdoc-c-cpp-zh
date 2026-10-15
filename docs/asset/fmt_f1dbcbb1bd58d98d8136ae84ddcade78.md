

```java
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
```

在软件世界中，我们将聚合对象定义为任何包含对其他对象作为实例数据的引用的对象。例如，`Account` 对象包含其他内容，其中包括一个表示账户所有者姓名的 `String` 对象。我们有时会忘记字符串是对象，但从技术上讲，这使得每个 `Account` 对象都成为一个聚合对象。

聚合是一种特殊的依赖关系。也就是说，部分由另一个类定义的类依赖于该类。聚合对象的方法通常调用其所组成的对象的方法。

让我们考虑另一个例子。Listing 7.5 所示的程序 `StudentBody` 创建了两个 `Student` 对象。每个 `Student` 对象部分由两个 `Address` 对象组成，一个用于学生在校的地址，另一个用于学生的家庭地址。`main` 方法除了创建 `Student` 对象并打印它们之外什么也不做。再次，我们将对象传递给 `println` 方法，依赖于对 `toString` 方法的自动调用来创建适合打印的对象的有效表示。

Listing 7.6 所示的 `Student` 类表示单个学生。如果要表示学生的所有方面，该类必须大幅扩展。我们现在故意保持其简单，以便清楚地显示对象聚合。`Student` 类的实例数据包括对两个 `Address` 对象的引用。我们在 `toString` 方法中引用这些对象，以创建学生的字符串表示。通过将 `Address` 对象连接到另一个字符串，`Address` 中的 `toString` 方法会被自动调用。

### LISTING 7.5

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

### OUTPUT

```text
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
```

### LISTING 7.6

```java
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

`Address` 类如 Listing 7.7 所示。它表示一个街道地址。请注意，`Address` 类中没有任何内容表明它是 `Student` 对象的一部分。`Address` 类的设计保持通用，因此可以在任何需要街道地址的情况下使用。

### LISTING 7.7

```java
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

对象越复杂，就越可能需要表示为聚合对象。在 UML 中，聚合由两个类之间的连接表示，在靠近聚合类的末端有一个开放的菱形。图 7.2 显示了 `StudentBody` 程序的 UML 类图。

请注意，在之前的 UML 图示例中以及图 7.2 中，字符串并未作为具有聚合关系的单独类表示，尽管从技术上讲它们可以。虽然字符串对编程至关重要，但在 UML 图中它们通常被表示为好像是原始类型一样。

## The `this` Reference

在我们离开类之间关系的主题之前，我们应该检查 Java 程序中使用的另一个特殊引用，称为 `this` 引用。`this` 是 Java 中的保留字。它允许对象引用自身。正如我们所讨论的，非静态方法是通过（或由）特定对象调用的

![](img/618a2d4ac82d0d6218f2b3b53b0b5d51_348_0.png)

或类中。在该方法内部，`this` 引用可用于指向当前正在执行的对象。

例如，在一个名为 `ChessPiece` 的类中，可能会有一个名为 `move` 的方法，其中可能包含以下代码行：

```java
if (this.position == piece2.position)
    result = false;
```

