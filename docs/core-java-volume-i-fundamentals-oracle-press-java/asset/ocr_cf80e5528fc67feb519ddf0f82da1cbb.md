```
```java
17    }
18
19    public double getSalary()
20    {
21        return salary;
22    }
23
24    public void raiseSalary(double byPercent)
25    {
26        double raise = salary * byPercent / 100;
27        salary += raise;
28    }
29
30    /**
31     * Compares employees by salary
32     * @param other another Employee object
33     * @return a negative value if this employee has a lower
       salary than
34     * otherObject, 0 if the salaries are the same, a positive
       value otherwise
35     */
36    public int compareTo(Employee other)
37    {
38        return Double.compare(salary, other.salary);
39    }
40    }
```
```

> > **java.lang.Comparable<T>** 1.0
> >
> > * `int compareTo(T other)`
> >
> > compares this object with other and returns a negative integer if this object is less than other, zero if they are equal, and a positive integer otherwise.

> > **java.util.Arrays** 1.2