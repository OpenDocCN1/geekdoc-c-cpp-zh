On many computers, a thread's **CurrentUICulture** and **CurrentCulture** properties will be set to the same **CultureInfo** object, which means that they both use the same language/country information. However, they can be set differently. For example: an application running in the United States could use Spanish for all of its menu items and other GUI elements while properly displaying all of the currency and date formatting for the United States. To do this, the thread's **CurrentUICulture** property should be set to a **CultureInfo** object initialized with a language of "es" (for Spanish), while the thread's **CurrentCulture** property should be set to a **CultureInfo** object initialized with a language/country pair of "en-US".

Internally, a **CultureInfo** object has a field that refers to a **System.Globalization.CompareInfo** object, which encapsulates the culture's character-sorting table information as defined by the Unicode standard. The following code demonstrates the difference between performing an ordinal comparison and a culturally aware string comparison:

```
    using System;
    using System.Globalization;

    public static class Program {
        public static void Main() {
            String s1 = "Strasse";
            String s2 = "Straße";
            Boolean eq;

            // CompareOrdinal returns nonzero.
            eq = String.Compare(s1, s2, StringComparison.Ordinal) == 0;
            Console.WriteLine("Ordinal comparison: '{0}' {2} '{1}'", s1, s2,
                eq ? "==" : "!=");

            // Compare Strings appropriately for people
            // who speak German (de) in Germany (DE)
            CultureInfo ci = new CultureInfo("de-DE");

            // Compare returns zero.
            eq = String.Compare(s1, s2, true, ci) == 0;
            Console.WriteLine("Cultural comparison: '{0}' {2} '{1}'", s1, s2,
                eq ? "==" : "!=");
        }
    }
```

Building and running this code produces the following output:

```
    Ordinal comparison: 'Strasse' != 'Straße'
    Cultural comparison: 'Strasse' == 'Straße'
```

> > **Note** When the **Compare** method is not performing an ordinal comparison, it performs *character expansions*. A character expansion is when a character is expanded to multiple characters regardless of culture. In the above case, the German Eszet character 'ß' is always expanded to 'ss'. Similarly, the 'Æ' ligature character is always expanded to 'AE'. So in the code example, the second call to Compare will always return 0 regardless of which culture I actually pass in to it.