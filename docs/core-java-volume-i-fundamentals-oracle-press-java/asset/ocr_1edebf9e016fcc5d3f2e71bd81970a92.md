```
```
public class Pair<T>
{
    public boolean equals(T value) { return first.equals(value)
&& second.equals(value); }
    . . .
}
```
```

Consider a Pair<String>. Conceptually, it has two equals methods:

```
```
boolean equals(String) // defined in Pair<T>
boolean equals(Object) // inherited from Object
```
```

But the intuition leads us astray. The erasure of the method

```
```
boolean equals(T)
```
```

is

```
```
boolean equals(Object)
```
```

which clashes with the Object.equals method.

The remedy is, of course, to rename the offending method.

The generics specification cites another rule: “To support translation by erasure, we impose the restriction that a class or type variable may not at the same time be a subtype of two interface types which are different parameterizations of the same interface.” For example, the following is illegal:

```
```
class Employee implements Comparable<Employee> { . . . }
class Manager extends Employee implements Comparable<Manager> {
    . . . } // ERROR
```
```

Manager would then implement both Comparable<Employee> and Comparable<Manager>, which are different parameterizations of the same