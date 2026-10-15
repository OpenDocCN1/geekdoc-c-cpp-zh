# LISTING 7.1 continued

```
System.out.println();
System.out.println ("Slogans created: " + Slogan.getCount());
}
```

# OUTPUT

+   Remember the Alamo.
+   Don't Worry. Be Happy.
+   Live Free or Die.
+   Talk is Cheap.
+   Write Once, Run Anywhere.
+   
+   Slogans created: 5

Listing 7.2 shows the Slogan class. The constructor of Slogan increments a static variable called count, which is initialized to zero when it is declared. Therefore, count serves to keep track of the number of instances of Slogan that are created.

The getCount method of Slogan is also declared as static, which allows it to be invoked through the class name in the main method. Note that the only data referenced in the getCount method is the integer variable count, which is static. As a static method, getCount cannot reference any nonstatic data.

The getCount method could have been declared without the static modifier, but then its invocation in the main method would have been done through an instance of the Slogan class instead of the class itself.

# LISTING 7.2

```
//******************************
// Slogan.java Author: Lewis/Loftus
// Represents a single slogan string.
//******************************

public class Slogan
{
    private String phrase;
    private static int count = 0;
}
```