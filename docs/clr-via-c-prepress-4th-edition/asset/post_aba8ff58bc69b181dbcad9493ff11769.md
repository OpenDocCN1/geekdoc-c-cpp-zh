
methods—CompareTo (required by the IComparable interface), CompareOrdinal, and the == and != operators—should also be avoided. The reason for avoiding these methods and operators is because the caller does not explicitly indicate how the string comparison should be performed, and you cannot determine from the name of the method what the default comparison will be. For example, by default, CompareTo performs a culture-sensitive comparison, whereas Equals performs an ordinal comparison. Your code will be easier to read and maintain if you always indicate explicitly how you want to perform your string comparisons.

Now, let’s talk about how to perform linguistically correct comparisons. The .NET Framework uses the System.Globalization.CultureInfo type to represent a language/country pair (as described by the RFC 1766 standard). For example, “en-US” identifies English as written in the United States, “en-AU” identifies English as written in Australia, and “de-DE” identifies German as written in Germany. In the CLR, every thread has two properties associated with it. Each of these properties refers to a CultureInfo object. The two properties are:

- **CurrentUICulture** This property is used to obtain resources that are shown to an end user. It is most useful for GUI or Web Forms applications because it indicates the language that should be used when displaying UI elements such as labels and buttons. By default, when you create a thread, this thread property is set to a CultureInfo object, which identifies the language of the Windows version that the application is running on using the Win32 GetUserDefaultUILanguage function. If you’re running a Multilingual User Interface (MUI) version of Windows, you can set this via the “Regional and Language Options” Control Panel Settings dialog box. On a non-MUI version of Windows, the language is determined by the localized version of the OS installed (or the installed language pack) and the language is not changeable.
- **CurrentCulture** This property is used for everything that CurrentUICulture isn’t used for, including number and date formatting, string casing, and string comparing. When formatting, both the language and country parts of the CultureInfo object are used. By default, when you create a thread, this thread property is set to a CultureInfo object, whose value is determined by calling the Win32 GetUserDefaultLocaleName method, whose value is set in the “Regional and Language” Control Panel applet.

For the two thread properties mentioned above, you can override the default value used by the system when a new thread gets created with AppDomain defaults by setting CultureInfo’s static DefaultThreadCurrentCulture and DefaultThreadCurrentUICulture properties.

On many computers, a thread’s CurrentUICulture and CurrentCulture properties will be set to the same CultureInfo object, which means that they both use the same language/country information. However, they can be set differently. For example: an application running in the United States could use Spanish for all of its menu items and other GUI elements while properly displaying all of the currency and date formatting for the United States. To do this, the thread’s CurrentUICulture property should be set to a CultureInfo object initialized with a language of “es” (for Spanish), while the thread’s CurrentCulture property should be set to a CultureInfo object initialized with a language/country pair of “en-US.”

Internally, a CultureInfo object has a field that refers to a System.Globalization.CompareInfo object, which encapsulates the culture’s character-sorting table information as defined by the Unicode standard. The following code demonstrates the difference between performing an ordinal comparison and a culturally aware string comparison:

```csharp
using System;
using System.Globalization;

public static class Program
{
    public static void Main()
    {
        String s1 = "Strasse";
        String s2 = "Straße";
        Boolean eq;

        // CompareOrdinal returns nonzero.
        eq = String.Compare(s1, s2, StringComparison.Ordinal) == 0;
        Console.WriteLine("Ordinal comparison: '{0}' {2} '{1}'", s1, s2,
            eq ? "==" : "!=");

        // Compare strings appropriately for people
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

**Note.** When the Compare method is not performing an ordinal comparison, it performs *character expansions*. A character expansion is when a character is expanded to multiple characters regardless of culture. In the above case, the German *Eszett* character ‘ß’ is always expanded to ‘ss.’ Similarly, the ‘Æ’ ligature character is always expanded to ‘AE.’ So in the code example, the second call to Compare will always return 0 regardless of which culture I actually pass in to it.

In some rare circumstances, you may need to have even more control when comparing strings for equality or sorting. This could be necessary when comparing strings consisting of Japanese characters. This additional control can be accessed via the CultureInfo object’s CompareInfo property. As mentioned earlier, a CompareInfo object encapsulates a culture’s character comparison tables, and there is just one CompareInfo object per culture.

When you call String’s Compare method, if the caller specifies a culture, the specified culture is used, or if no culture is specified, the value in the calling thread’s CurrentCulture property is used. Internally, the Compare method obtains the reference to the CompareInfo object for the appropriate culture and calls the Compare method of the CompareInfo object, passing along the appropriate options (such as case insensitivity). Naturally, you could call the Compare method of a specific CompareInfo object yourself if you need the additional control.

The Compare method of the CompareInfo type takes as a parameter a value from the CompareOptions enumerated type (as shown earlier). You can OR these bit flags together to gain significantly greater control over formatting when comparing strings. For a complete description of these symbols, consult the .NET Framework documentation.

The following code demonstrates how important culture is to sorting strings and shows various ways of performing string comparisons:

```csharp
using System;
using System.Text;
using System.Windows.Forms;
using System.Globalization;
using System.Threading;

public sealed class Program {
    public static void Main() {
        String output = String.Empty;
        String[] symbol = new String[] { "<", "=", ">" };
        Int32 x;
        CultureInfo ci;

        // The code below demonstrates how strings compare
        // differently for different cultures.
        String s1 = "coté";
        String s2 = "côte";

        // Sorting strings for French in France.
        ci = new CultureInfo("fr-FR");
        x = Math.Sign(ci.CompareInfo.Compare(s1, s2));
        output += String.Format("{0} Compare: {1} {2} {3}",
            ci.Name, s1, s2, symbol[x + 1]);
        output += Environment.NewLine;

        // Sorting strings for Japanese in Japan.
        ci = new CultureInfo("ja-JP");
        x = Math.Sign(ci.CompareInfo.Compare(s1, s2));
        output += String.Format("{0} Compare: {1} {2} {3}",
            ci.Name, s1, s2, symbol[x + 1]);
        output += Environment.NewLine;

        // Sorting strings for the thread's culture
        ci = Thread.CurrentThread.CurrentCulture;
        x = Math.Sign(ci.CompareInfo.Compare(s1, s2));
        output += String.Format("{0} Compare: {1} {2} {3}",
            ci.Name, s1, s2, symbol[x + 1]);
        output += Environment.NewLine + Environment.NewLine;
    }
}
```
