
### Table 7.7 Differences between Decomposition Modes

| No Decomposition | Canonical Decomposition | Full Decomposition |
|---|---|---|
| Ä ≠ Å | Ä = Å | Ä = Å |
| ™ ≠ TM | ™ ≠ TM | ™ = TM |

It is wasteful to have the collator decompose a string many times. If one string is compared against other strings many times, you can save the decomposition in a collation key object. The getCollationKey method returns a CollationKey object that you can use for further, faster comparisons. Here is an example:

```java
String a = "...";
CollationKey aKey = coll.getCollationKey(a);
if (aKey.compareTo(coll.getCollationKey(b)) == 0) // fast comparison
    ...
```

Finally, you might want to convert strings into their normalized forms even if you don’t do collation—for example, to store strings in a database or communicate with another program. The java.text.Normalizer class carries out the normalization process. For example,

```java
String name = "Ångström";
String normalized = Normalizer.normalize(name, Normalizer.Form.NFD); // uses normalization
                                                                  // form D
```

The normalized string contains ten characters. The “Å” and “ö” are replaced by “Å” and “ö” sequences.

However, that is not usually the best form for storage and transmission. Normalization form C first applies decomposition and then combines the accents back in a standardized order. According to the W3C, this is the recommended mode for transferring data over the Internet.

The program in Listing 7.4 lets you experiment with collation order. Type a word into the text field and click the Add button to add it to the list of words. Each time you add another word, or change the locale, strength, or decomposition mode, the list of words is sorted again. An = sign indicates words that are considered identical (see Figure 7.3).

The locale names in the combo box are displayed in sorted order, using the collator of the default locale. If you run this program with the US English locale, note that “Norwegian (Nynorsk)” comes before “Norwegian (Norway),” even though the Unicode value of the comma character is greater than the Unicode value of the closing parenthesis.

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_427_0.png)

**Figure 7.3** The CollationTest program

### Listing 7.4 `collation/CollationTest.java`

```java
package collation;

import java.awt.*;
import java.awt.event.*;
import java.text.*;
import java.util.*;
import java.util.List;

import javax.swing.*;

/**
 * This program demonstrates collating strings under various locales.
 * @version 1.10 2018-05-01
 * @author Cay Horstmann
 */
public class CollationTest
{
    public static void main(String[] args)
    {
        EventQueue.invokeLater(() ->
        {
            var frame = new CollationFrame();
            frame.setTitle("Collation Test");
            frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            frame.setVisible(true);
        });
    }

    /**
     * This frame contains combo boxes to pick a locale, collation strength and decomposition
     * rules, a text field and button to add new strings, and a text area to list the collated
     * strings.
     */
    class CollationFrame extends JFrame
    {
        private Collator collator = Collator.getInstance(Locale.getDefault());
        private List<String> strings = new ArrayList<>();
        private Collator currentCollator;
        private Locale[] locales;
        private JComboBox<String> localeCombo = new JComboBox<>();
        private JTextField newWord = new JTextField(20);
        private JTextArea sortedWords = new JTextArea(20, 20);
        private JButton addButton = new JButton("Add");
        private EnumCombo<Integer> strengthCombo = new EnumCombo<>(Collator.class, "Primary",
                "Secondary", "Tertiary", "Identical");
        private EnumCombo<Integer> decompositionCombo = new EnumCombo<>(Collator.class,
                "Canonical Decomposition", "Full Decomposition", "No Decomposition");

        public CollationFrame()
        {
            setLayout(new GridBagLayout());
            add(new JLabel("Locale"), new GBC(0, 0).setAnchor(GBC.EAST));
            add(new JLabel("Strength"), new GBC(0, 1).setAnchor(GBC.EAST));
            add(new JLabel("Decomposition"), new GBC(0, 2).setAnchor(GBC.EAST));
            add(addButton, new GBC(0, 3).setAnchor(GBC.EAST));
            add(localeCombo, new GBC(1, 0).setAnchor(GBC.WEST));
            add(strengthCombo, new GBC(1, 1).setAnchor(GBC.WEST));
            add(decompositionCombo, new GBC(1, 2).setAnchor(GBC.WEST));
            add(newWord, new GBC(1, 3).setFill(GBC.HORIZONTAL));
            add(new JScrollPane(sortedWords), new GBC(0, 4, 2, 1).setFill(GBC.BOTH));

            locales = (Locale[]) Collator.getAvailableLocales().clone();
            Arrays.sort(locales,
                    (l1, l2) -> collator.compare(l1.getDisplayName(), l2.getDisplayName()));

            for (Locale loc : locales)
                localeCombo.addItem(loc.getDisplayName());
            localeCombo.setSelectedItem(Locale.getDefault().getDisplayName());

            strings.add("America");
            strings.add("able");
            strings.add("Zulu");
            strings.add("zebra");
            strings.add("\u00c5ngstr\u00f6m");
            strings.add("A\u030angstr\u00f6m");
            strings.add("Angstrom");
            strings.add("Able");
            strings.add("office");
            strings.add("o\uFB03ce");
            strings.add("Java\u2122");
            strings.add("Java™");
            updateDisplay();

            addButton.addActionListener(event ->
                {
                    strings.add(newWord.getText());
                    updateDisplay();
                });

            ActionListener listener = event -> updateDisplay();

            localeCombo.addActionListener(listener);
            strengthCombo.addActionListener(listener);
            decompositionCombo.addActionListener(listener);
            pack();
        }

        /**
         * Updates the display and collates the strings according to the user settings.
         */
        public void updateDisplay()
        {
            Locale currentLocale = locales[localeCombo.getSelectedIndex()];
            localeCombo.setLocale(currentLocale);

            currentCollator = Collator.getInstance(currentLocale);
            currentCollator.setStrength(strengthCombo.getValue());
            currentCollator.setDecomposition(decompositionCombo.getValue());

            strings.sort(currentCollator);

            sortedWords.setText("");

            for (int i = 0; i < strings.size(); i++)
            {
                String s = strings.get(i);
                if (i > 0 && s.compareToIgnoreCase(strings.get(i - 1)) == 0)
                    sortedWords.append("=");
                sortedWords.append(s + "\n");
            }
            pack();
        }
    }
}
```

### `java.text.Collator` 1.1

- `static Locale[] getAvailableLocales()`  
  returns an array of Locale objects for which Collator objects are available.
- `static Collator getInstance()`
- `static Collator getInstance(Locale l)`  
  returns a collator for the default locale or the given locale.
- `int compare(String a, String b)`  
  returns a negative value if a comes before b, 0 if they are considered identical, and a positive value otherwise.
- `boolean equals(String a, String b)`  
  returns true if a and b are considered identical, false otherwise.
- `void setStrength(int strength)`
- `int getStrength()`  
  sets or gets the strength of the collator. Stronger collators tell more words apart. Strength values are `Collator.PRIMARY`, `Collator.SECONDARY`, and `Collator.TERTIARY`.
- `void setDecomposition(int decomp)`
- `int getDecomposition()`  
  sets or gets the decomposition mode of the collator. The more a collator decomposes a string, the more strict it will be in deciding whether two strings should be considered identical. Decomposition values are `Collator.NO_DECOMPOSITION`, `Collator.CANONICAL_DECOMPOSITION`, and `Collator.FULL_DECOMPOSITION`.
- `CollationKey getCollationKey(String a)`  
  returns a collation key that contains a decomposition of the characters in a form that can be quickly compared against another collation key.

**NOTE:** This example shows that the designer of the choice format was a bit muddleheaded. If you have three format strings, you need two limits to separate them. In general, you need one fewer limit than you have format strings. As you saw in Table 7.8, the `MessageFormat` class ignores the first limit.

The syntax would have been a lot clearer if the designer of this class realized that the limits belong between the choices, such as

```text
no houses|1|one house|2{1} houses // not the actual format
```

You can use the `<` symbol to denote that a choice should be selected if the lower bound is strictly less than the value.

You can also use the ≤ symbol (expressed as the Unicode character code `\u2264`) as a synonym for `#`. If you like, you can even specify a lower bound of −∞ as `-\u221E` for the first value.

For example,

```text
-∞#no houses|0#one house|2<{1} houses
```

or, using Unicode escapes,

```text
-\u221E\u2264no houses|0\u2264one house|2<{1} houses
```

Let's finish our natural disaster scenario. If we put the choice string inside the original message string, we get the following format instruction:

```java
String pattern = "On {2,date,long}, {0} destroyed {1,choice,0#no houses|1#one house|2<{1}
  houses}" + " and caused {3,number,currency} of damage.";
```

Or, in German,

```java
String pattern
    = "{0} zerstörte am {2,date,long} {1,choice,0#kein Haus|1#ein Haus|2#{1} Häuser}"
      + " und richtete einen Schaden von {3,number,currency} an.";
```

Note that the ordering of the words is different in German, but the array of objects you pass to the format method is the same. The order of the placeholders in the format string takes care of the changes in the word ordering.

## 7.6 Text Input and Output

As you know, the Java programming language itself is fully Unicode-based. However, Windows and Mac OS X still support legacy character encodings such as Windows-1252 or Mac Roman in Western European countries, or Big5 in Taiwan. Therefore, communicating with your users through text is
