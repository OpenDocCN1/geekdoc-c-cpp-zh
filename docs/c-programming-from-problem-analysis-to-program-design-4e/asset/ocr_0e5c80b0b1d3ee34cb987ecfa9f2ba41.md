25. The following program has several syntax errors as well as style inconsistencies. Correct the syntax errors and identify the style violations.

```
public class Chair
{
    private string type;
    private double weight;
    private double cost;
    private Chair()
    {
    }
    private Chair(weight, type, cost)
    {
    }
    public string ChairType
    {
        get
        {
            return type;
        }
        set
        {
            ChairType = value;
        }
    }
    public override ToString()
    {
        return "Type of Chair: " + ChairType;
    }
}
```

# PROGRAMMING EXERCISES

+   1. Create a class representing a student. Include characteristics such as student number, first and last name, overall GPA, classification, and major. Write at least two constructors. Include properties for each of the data items. Create a second class that instantiates the first class with information about yourself. In the second class, create a class method that displays your name and GPA.

+   2. Create a Motorway class that can be used as extra documentation with directions. Include data members such as name of motorway, type (i.e., Road, Street, Avenue, Blvd., Lane, etc.), direction (i.e., E, W, N, or S), surface (i.e., blacktop, gravel, sand, concrete), number of lanes, toll or no toll, and the party that maintains it. Write instance methods that returns the full name of the motorway, full name of the motorway and whether it is toll or not, and full name of the motorway and the number of lanes. Also include a ToString( ) method that returns all data members with appropriate labels. Include enough constructors to make the class flexible and experiment with using the class diagram to create the property members.