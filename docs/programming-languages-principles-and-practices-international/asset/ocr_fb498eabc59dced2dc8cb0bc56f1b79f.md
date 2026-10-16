```
results.add(strategy.transform(element));
return results;
}catch(Exception e){
    System.out.println(e);
    return null;
}
}
```

As mentioned earlier, the user of one of our new iterators is responsible for supplying a collection and an instance of the corresponding strategy interface. The programmer could define a new class that implements MapStrategy, FilterStrategy, or ReduceStrategy, but there is no need to go to that trouble. Java allows the programmer to create an instance of an anonymous class at the point of use, in much the same manner as functional programmers create lambda forms. The syntax for this is:

```
new <interface name>(){
    <method implementations>
}
```

Table 5.4 shows the MapStrategy interface and an example instantiation. The instantiation transforms an integer value into a double value by taking the square root of the integer.

**Table 5.4  The MapStrategy interface and an instantiation**

| Interface | Instantiation |
|---|---|
| `public interface MapStrategy<E, R>{`<br>&nbsp;&nbsp;&nbsp;&nbsp;`public R transform(E element);`<br>`}` | `new MapStrategy<Integer, Double>(){`<br>&nbsp;&nbsp;&nbsp;&nbsp;`public Double transform(Integer i){`<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`return Math.sqrt(i);`<br>&nbsp;&nbsp;&nbsp;&nbsp;`}`<br>`}` |

The next code segment shows a complete application that takes our new iterators for a test drive. Note that two different particular mapping strategies are used, and then one filtering strategy and one reducing strategy. The same code could be used on a set of integers or on any other collection class (like the LinkedStack explored in Section 5.3.2) of integers.

```
import iterators.*;
import java.util.*;

/*
Tests the map, filter, and reduce iterators with array lists.
Creates strategy objects as anonymous instances of the appropriate interfaces.
*/

public class TestIterators{

    static public void main(String[] args){
```