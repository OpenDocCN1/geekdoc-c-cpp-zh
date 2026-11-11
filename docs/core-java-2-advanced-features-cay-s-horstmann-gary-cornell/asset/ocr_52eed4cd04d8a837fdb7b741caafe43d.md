![](bbox=[0.129, 0.14, 0.784, 0.509])

Figure 9.4  Modifying bytecodes with a hex editor

# Listing 9.3  `verifier/VerifierTest.java`

```
```java
package verifier;

import java.applet.*;
import java.awt.*;

/**
 * This application demonstrates the bytecode verifier of the virtual machine. If you use a hex
 * editor to modify the class file, then the virtual machine should detect the tampering.
 * @version 1.00 1997-09-10
 * @author Cay Horstmann
 */
public class VerifierTest extends Applet
{
    public static void main(String[] args)
    {
        System.out.println("1 + 2 == " + fun());
    }
}
```
```