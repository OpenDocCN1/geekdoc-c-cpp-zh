# Example 187 Numbers to a Text File

Simulate 1000 rolls of a die and print the outcome to the text file dice.txt. 20 numbers to a line. It is important to close the text writer after writing; otherwise some or all of the output may be lost.

```
using System;
using System.IO;

public class TextWriterExample {
    public static void Main() {
        TextWriter tw = new StreamWriter("dice.txt");
        Random rand = new Random();
        for (int i=0; i<=100; i++) {
            int die = (int)(1 + 6 * rand.NextDouble());
            tw.Write(die); tw.Write(' ');
            if (i % 20 == 0) tw.WriteLine();
        }
        tw.Close(); // Without this, the output file may be empty
    }
}
```

# Example 188 Printing an HTML Table

This example generates a temperature conversion table in HTML. The Fahrenheit temperature $f$ corresponds to the Celsius temperature $c=5·(f-32)/9$. The number of fractional digits is controlled by format specifications ({0:#} and {1:0.0}) (see section 7.2). The HTML table tag is used to control the alignment of numbers columns.

```
TextWriter tw = new StreamWriter(new FileStream("temperature.html", FileMode.Create));
tw.WriteLine("<table><tr><th>Fahrenheit</th><th>Celsius</th></tr>");
for (double f=100; f<=400; f+=10) {
    double c = 5 * (f - 32) / 9;
    tw.WriteLine("<tr align="right"><td>{0:#}</td><td>{1:0.0}</td></tr>", f, c);
}
tw.WriteLine("</table>");
t.Close(); // Without this, the output file may be
```

# Example 189 Printing a Text Table

To write a conversion table in text format in a fixed-pitch font, replace the format specifications in example 188 by {0,10:#} and {1,10:0.0} and delete the HTML tags. See section 7.2 for more formatting codes.