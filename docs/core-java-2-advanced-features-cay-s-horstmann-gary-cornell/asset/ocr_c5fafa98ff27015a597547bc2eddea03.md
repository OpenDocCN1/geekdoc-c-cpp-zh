**NOTE:** It is possible to support a more complex two-phase protocol, whereby a login is committed if all modules in the login configuration were successful. For more information, see the login module developer’s guide at http://docs.oracle.com/javase/8/docs/technotes/guides/security/jaas/JAASLMDevGuide.html.

# **Listing 9.10** `jaas/SimplePrincipal.java`

```
```java
package jaas;

import java.security.*;
import java.util.*;

/**
 * A principal with a named value (such as "role=HR" or "username=harry").
 */
public class SimplePrincipal implements Principal
{
    private String descr;
    private String value;

    /**
     * Constructs a SimplePrincipal to hold a description and a value.
     * @param descr the description
     * @param value the associated value
     */
    public SimplePrincipal(String descr, String value)
    {
        this.descr = descr;
        this.value = value;
    }

    /**
     * Returns the role name of this principal.
     * @return the role name
     */
    public String getName()
    {
        return descr + "=" + value;
    }

    public boolean equals(Object otherObject)
    {
        if (this == otherObject) return true;
        if (otherObject == null) return false;
        if (getClass() != otherObject.getClass()) return false;
        SimplePrincipal other = (SimplePrincipal) otherObject;
        return Objects.equals(getName(), other.getName());
    }
}
```
```