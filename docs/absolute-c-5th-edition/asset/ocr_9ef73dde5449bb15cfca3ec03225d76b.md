# 656 CHAPTER 14 Inheritance

in Display 14.4. A Doctor record has the doctor's specialty (such as Pediatric, Obstetrician, General Practitioner, et., so use type string), and office fee (type double). Be sure your class has a reasonable complement of constructors and accessor methods, an overloaded assignment operator, and a copy constructor. Write a driver program to test all your methods.

+   4. Create a base class Vehicle that has the manufacturer's name (type string), number of cylinders in the engine (type int), and owner (type Person) given in the code that follows. Then create a class Truck that is derived from Vehicle and has additional properties, the load capacity in tons (type double once since it may contain a fractional part) and towing capacity in pounds (type int). Be sure your classes have a reasonable complement of constructors and accessor methods, an overloaded assignment operator, and a copy constructor. Write a driver program to test all your methods.

The definition of the class Person follows. The implementation of the class is part of this programming project.

```
class Person {
public:
    Person();
    Person(string theName);
    Person(const Person& theObject);
    string getName() const;
    Person& operator=(const Person& rtSide);
    friend istream operator&(istream& inStream, Person& personObject);
    friend ostream operator<<(ostream& outStream, const Person& personObject);

private:
    string name;
}
```

+   5. Give the definition of two classes, Patient and Billing, whose objects are records for a clinic. Patient will be derived from the class Person given in Programming Project 14.4. A Patient record has the patient's name (inherited from the class Person) and primary physician, of type Doctor defined in Programming Project 14.3. A Billing object will contain a Patient object and a Doctor object, and an amount of type double. Be sure your classes have a reasonable complement of constructors and accessor methods, an overloaded assignment operator, and a copy constructor. Write a driver program to test all of your methods, write a test program that creates at least two patients, at least two doctors, at least two Billing records, then prints out the income from the Billing records.

+   6. Define a class Payment that contains a member variable of type float that stores the amount of the payment and appropriate accessor and mutator functions. Also create a member function paymentDetails that outputs an English sentence describing the amount of the payment.