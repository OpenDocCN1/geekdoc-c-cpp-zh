```

    /**
     * Sets the alpha of the source.
     * @param a the alpha value between 0 and 100
     */
    public void setAlpha(int a)
    {
        alpha = (float) a / 100.0F;
        repaint();
    }
    }
```

# **Listing 11.5** composite/Rule.java

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
```

*(Continues)*