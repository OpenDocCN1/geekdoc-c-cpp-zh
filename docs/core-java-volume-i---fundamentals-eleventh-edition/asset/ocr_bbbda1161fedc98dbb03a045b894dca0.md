# Listing 5.9 (Continued)

```
```java
54    // test whether the fields have identical values
55    return Objects.equals(name, other.name)
56        && salary == other.salary && Objects.equals(hireDay, other.hireDay);
57  }
58
59  public int hashCode()
60  {
61      return Objects.hash(name, salary, hireDay);
62  }
63
64  public String toString()
65  {
66      return getClass().getName() + "[name=" + name + ",salary=" + salary + ",hireDay="
67          + hireDay + "]";
68  }
69  }
```
```

# Listing 5.10 equals/Manager.java

```
```java
1  package equals;
2
3  public class Manager extends Employee
4  {
5      private double bonus;
6
7      public Manager(String name, double salary, int year, int month, int day)
8      {
9          super(name, salary, year, month, day);
10         bonus = 0;
11     }
12
13     public double getSalary()
14     {
15         double baseSalary = super.getSalary();
16         return baseSalary + bonus;
17     }
18
19     public void setBonus(double bonus)
20     {
21         this.bonus = bonus;
22     }
23 }
```
```