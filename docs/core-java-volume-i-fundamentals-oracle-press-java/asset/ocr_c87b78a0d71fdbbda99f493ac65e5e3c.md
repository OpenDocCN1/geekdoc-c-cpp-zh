```
```java
 9  */
10  public class EmployeeSortTest
11  {
12      public static void main(String[] args)
13      {
14          var staff = new Employee[3];
15  
16          staff[0] = new Employee("Harry Hacker", 35000);
17          staff[1] = new Employee("Carl Cracker", 75000);
18          staff[2] = new Employee("Tony Tester", 38000);
19  
20          Arrays.sort(staff);
21  
22          // print out information about all Employee objects
23          for (Employee e : staff)
24              System.out.println("name=" + e.getName() + ",salary="
+ e.getSalary());
25      }
26  }
```
```

# **Listing 6.2** interfaces/Employee.java

```
```java
 1  package interfaces;
 2  
 3  public class Employee implements Comparable<Employee>
 4  {
 5      private String name;
 6      private double salary;
 7  
 8      public Employee(String name, double salary)
 9      {
10          this.name = name;
11          this.salary = salary;
12      }
13  
14      public String getName()
15      {
16          return name;
```
```