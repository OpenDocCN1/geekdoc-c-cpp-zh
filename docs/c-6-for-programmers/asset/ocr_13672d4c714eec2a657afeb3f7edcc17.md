# CommissionEmployee Constructor

Constructors are not inherited, so class CommissionEmployee does not inherit class object's constructor. However, class CommissionEmployee's constructor calls object's constructor implicitly. In fact, before executing the code in its own body, every derived class's constructor calls a constructor in its direct base class, either explicitly or implicitly (if no constructor call is specified), to ensure that the instance variables inherited from the base class are initialized properly.

Calling a base-class constructor explicitly is discussed in Section 11.4.3. If the code does not explicitly call the base-class constructor, the compiler generates an implicit call to the base class's default or parameterless constructor, or a constructor with all default arguments. The comment in line 18 indicates where the implicit call to the base class object's constructor is made (you do not write the code for this call). Even if a base class does not have constructors, the default constructor that the compiler implicitly declares for the class will call the base class's default or parameterless constructor. Class object is the only class that does not have a base class.

After the implicit call to object's constructor occurs, lines 19–23 in the constructor assign values to the class's properties. We do not validate the values of arguments first—Name, lastName and socialSecurityNumber. We certainly could validate the first and last names—perhaps by ensuring that they're of a reasonable length. Similarly, a social security number could be validated to ensure that it contains nine digits, with or without dashes (e.g., 123-45-6789 or 123456789).

# CommissionEmployee Method Earnings

Method Earnings (line 65) calculates a CommissionEmployee's earnings by multiplying the commissionRate and the grossSales, then returns the result. As a best practice, we should use the properties CommissionRate and GrossSales to access the instance variables in line 65. We access them directly here and in the next few examples to help motivate then demonstrate the protected access modifier. In this chapter's final example, we'll follow best practice.

# CommissionEmployee Method ToString

Method ToString (lines 68–72) is special—it's one of the methods that every class inherits directly or indirectly from class object. Method ToString returns a string representing an object. It can be called explicitly, but it's called implicitly by an app whenever an object must be converted to a string representation, such as when displaying an object with Console's Write or WriteLine methods or inserting an object in a string-interpolation expression. By default, class object's ToString method returns the object's fully qualified class name. For object, ToString returns

```
System.Object
```

because object is an alias for class Object in the System namespace. ToString is primarily a placeholder that can be (and typically should be) overridden by a derived class to specify an appropriate string representation of the data in a derived class object.

Method ToString of class CommissionEmployee overrides (redefines) class object's ToString method. When invoked, CommissionEmployee's ToString method returns a string containing information about the CommissionEmployee. Line 71 uses the format