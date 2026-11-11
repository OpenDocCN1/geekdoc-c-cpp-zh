The hashCode method is defined in the Object class. Therefore, every object has a default hash code. That hash code is derived from the object’s memory address. Consider this example:

```
var s = "Ok";
var sb = new StringBuilder(s);
System.out.println(s.hashCode() + " " + sb.hashCode());
var t = new String("Ok");
var tb = new StringBuilder(t);
System.out.println(t.hashCode() + " " + tb.hashCode());
```

Table 5.2 shows the result.

# Table 5.2  Hash Codes of Strings and String Builders

| Object | Hash Code | Object | Hash Code |
|---|---:|---|---:|
| s | 2556 | t | 2556 |
| sb | 20526976 | tb | 20527144 |

Note that the strings s and t have the same hash code because, for strings, the hash codes are derived from their contents. The string builders sb and tb have different hash codes because no hashCode method has been defined for the StringBuilder class and the default hashCode method in the Object class derives the hash code from the object’s memory address.

If you redefine the equals method, you will also need to redefine the hashCode method for objects that users might insert into a hash table. (We discuss hash tables in Chapter 9.)

The hashCode method should return an integer (which can be negative). Just combine the hash codes of the instance fields so that the hash codes for different objects are likely to be widely scattered.

For example, here is a hashCode method for the Employee class:

```
public class Employee
{
    public int hashCode()
    {
        return 7 * name.hashCode()
             + 11 * new Double(salary).hashCode()
             + 13 * hireDay.hashCode();
    }
    . . . .
}
```