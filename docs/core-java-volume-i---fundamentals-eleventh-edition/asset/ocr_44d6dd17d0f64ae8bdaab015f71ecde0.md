```
```java
public double getSalary()
{
    return salary;
}

public LocalDate getHireDay()
{
    return hireDay;
}

public void raiseSalary(double byPercent)
{
    double raise = salary * byPercent / 100;
    salary += raise;
}
```
```

# ### 4.3.2 Use of Multiple Source Files

The program in Listing 4.2 has two classes in a single source file. Many programmers prefer to put each class into its own source file. For example, you can place the Employee class into a file Employee.java and the EmployeeTest class into EmployeeTest.java.

If you like this arrangement, you have two choices for compiling the program. You can invoke the Java compiler with a wildcard:

```
```bash
javac Employee*.java
```
```

Then, all source files matching the wildcard will be compiled into class files. Or, you can simply type

```
```bash
javac EmployeeTest.java
```
```

You may find it surprising that the second choice works even though the Employee.java file is never explicitly compiled. However, when the Java compiler sees the Employee class being used inside EmployeeTest.java, it will look for a file named Employee.class. If it does not find that file, it automatically searches for Employee.java and compiles it. Moreover, if the timestamp of the version of Employee.java that it finds is newer than that of the existing Employee.class file, the Java compiler will automatically recompile the file.

> > **NOTE:** If you are familiar with the make facility of UNIX (or one of its Windows cousins, such as nmake), you can think of the Java compiler as having the make functionality already built in.