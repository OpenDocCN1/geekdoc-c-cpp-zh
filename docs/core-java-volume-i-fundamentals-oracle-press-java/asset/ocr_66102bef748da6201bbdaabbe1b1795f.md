```
```java
12    */
13    public class Employee
14    {
15        private String name;
16        private double salary;
17        private LocalDate hireDay;
18
19        public Employee(String name, double salary, int year, int
   month, int day)
20        {
21            this.name = name;
22            this.salary = salary;
23            hireDay = LocalDate.of(year, month, day);
24        }
25
26        public String getName()
27        {
28            return name;
29        }
30
31        public double getSalary()
32        {
33            return salary;
34        }
35
36        public LocalDate getHireDay()
37        {
38            return hireDay;
39        }
40
41        public void raiseSalary(double byPercent)
42        {
43            double raise = salary * byPercent / 100;
44            salary += raise;
45        }
46    }
```
```

# 4.8.5 Package Access