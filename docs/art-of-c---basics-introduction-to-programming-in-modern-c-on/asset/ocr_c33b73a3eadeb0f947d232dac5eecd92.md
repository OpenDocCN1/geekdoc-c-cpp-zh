solutions. One can probably implement this more efficiently using a better algorithm.

```
morse-code/Decoder.cs
namespace Morse;
using System.Text;

public static class Decoder {
    public static string Decode(string cipher) {
        var sb = new StringBuilder();

        var code = new StringBuilder();
        var spaceCount = 0;
        foreach (var c in cipher) {
            if (c == ' ') {
                ++spaceCount;
            } else {
                if (spaceCount > 0) {
                    AddChar(sb, code);

                    if (spaceCount > 1) {
                        sb.Append(' ');
                    }
                    spaceCount = 0;
                }
                code.Append(c);
            }
        }
        AddChar(sb, code);

        return sb.ToString();
    }

    private static void AddChar(StringBuilder sb, StringBuilder code)
    {
        if (code.Length > 0) {
            try {
```