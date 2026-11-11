# **Listing 11.19** `composite/Rule.java`

```
package composite;

import java.awt.*;

/**
 * This class describes a Porter-Duff rule.
 */
class Rule
{
    private String name;
    private String porterDuff1;
    private String porterDuff2;

    /**
     * Constructs a Porter-Duff rule.
     * @param n the rule name
     * @param pd1 the first row of the Porter-Duff square
     * @param pd2 the second row of the Porter-Duff square
     */
    public Rule(String n, String pd1, String pd2)
    {
        name = n;
        porterDuff1 = pd1;
        porterDuff2 = pd2;
    }

    /**
     * Gets an explanation of the behavior of this rule.
     * @return the explanation
     */
    public String getExplanation()
    {
        var r = new StringBuilder("Source ");
        if (porterDuff2.equals("0")) r.append("clears");
        if (porterDuff2.equals("S")) r.append("overwrites");
        if (porterDuff2.equals("DS")) r.append("blends with");
        if (porterDuff2.equals("D")) r.append("alpha modifies");
        if (porterDuff2.equals("1-D")) r.append("alpha complement modifies");
        if (porterDuff2.equals("1")) r.append("does not affect");
        r.append(" destination");
        if (porterDuff1.equals("S")) r.append(" and overwrites empty pixels");
        r.append(".");
        return r.toString();
    }
}
```

_(Continues)_