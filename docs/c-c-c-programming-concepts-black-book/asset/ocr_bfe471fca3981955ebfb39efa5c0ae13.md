```
```csharp
empList.Add(new Employee(700, "Bill", "USA"));
empList.Add(new Employee(600, "Keith", "UK"));

var empSel = from emp in empList
             group emp by emp.empCity into empCityGrp
             select new { cityName = empCityGrp.Key,
                          empDet = empCityGrp };

foreach (var e in empSel)
{
    Console.WriteLine("City Name: {0}", e.cityName);

    foreach (var emp in e.empDet)
    {
        Console.WriteLine("Employee ID: {0}\n            Employee Name: {1}", emp.empID, emp.empName);
    }
}
}

class Employee
{
    public int empID;
    public string empName;
    public string empCity;

    public Employee()
    {
    }

    public Employee(int id, string name, string city)
    {
        this.empID = id;
        this.empName = name;
        this.empCity = city;
    }
}
```
```

The preceding program returns a list of employees grouped by their city name. For this operation, we first get the sequence of employee details grouped by city names. By using the outer foreach loop, we first print the name of a city on the console. After that, we print the employee details on the console for that specific city name by using the inner foreach loop. The output of the program is given as follows:

```
```text
City Name: Canada
Employee ID: 100 Employee Name: Mathew
Employee ID: 400 Employee Name: Albert
City Name: USA
Employee ID: 200 Employee Name: John
Employee ID: 800 Employee Name: Joseph
Employee ID: 700 Employee Name: Bill
City Name: UK
Employee ID: 500 Employee Name: Marry
Employee ID: 600 Employee Name: Keith
```
```

In the preceding example, we have used an anonymous type to explain the GroupBy execution.