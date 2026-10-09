# morse-code/Encoder.cs

```
namespace Morse;
using System.Text;

public static class Encoder {
    public static string Encode(string text) {
        var sb = new StringBuilder();

        foreach (var c in text) {
            if (Code.MorseCode.ContainsKey(c)) {
                var v = Code.MorseCode[c];
                sb.Append(v).Append(' ');
            } else {
                if (c == ' ') {
                    sb.Append("  ");
                } else {
                    sb.Append("???");
                }
            }
        }

        return sb.ToString();
    }
}
```

# morse-code/Decoder.cs

```
namespace Morse;
using System.Text;

public static class Decoder {
    public static string Decode(string cipher) {
        var sb = new StringBuilder();

        var code = new StringBuilder();
        var spaceCount = 0;
        foreach (var c in cipher) {
```