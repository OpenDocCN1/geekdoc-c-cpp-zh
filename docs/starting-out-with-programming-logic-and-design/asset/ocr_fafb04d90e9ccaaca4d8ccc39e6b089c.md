# Chapter 14 Object-Oriented Programming

Now let's identify the class's methods. In this program, what must the Car class do? Once again, the only obvious actions are the standard set of methods that we will find in most classes (constructors, accessors, and mutators). Specifically, the actions are as follows:

+   - create an object of the Car class
- set and get the car's make
- set and get the car's model
- set and get the car's year

Figure 14-15 shows a UML diagram for the Car class, and Class Listing 14-6 shows the pseudocode for a class definition.

Figure 14-15 UML diagram for the Car class

| Car |
| - make : String
| - model : String
| - year : Integer |
| + Car(carMake: String, carModel: String, carYear: Integer)
| + setMake(m : String)
| + setModel(m : String)
| + setYear(y : Integer)
| + getMake() : String
| + getModel() : String
| + getYear() : Integer |

# Class Listing 14-6

```
1 Class Car
2 // Fields
3 Private String make
4 Private String model
5 Private Integer year
6 
7 
8 // Constructor
9 Public Module Car(String carMake,
10 String carModel, Integer carYear)
11 Set make = carMake
12 Set model = carModel
13 Set year = carYear
14 End Module
15 // Mutators
16 Public Module setMake(String m)
17 Set make = m
18 End Module
19 
20 Public Module setModel(String m)
21 Set model = m
22 End Module
```