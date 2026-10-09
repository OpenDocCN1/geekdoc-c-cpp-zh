```
internal static string ToNumeralString(ushort number) {
    var sb = new StringBuilder();

    while (number > 0) {
        if (number >= 1000) {
            sb.Append(number switch {
                >= 3000 => "MMMM",
                >= 2000 => "MMM",
                _ => "M",
            });
            number %= 1000;
        } else if (number >= 100) {
            sb.Append(number switch {
                >= 900 => "CM",
                >= 800 => "DCCC",
                >= 700 => "DCC",
                >= 600 => "DC",
                >= 500 => "D",
                >= 400 => "CD",
                >= 300 => "CCC",
                >= 200 => "CC",
                _ => "C",
            });
            number %= 100;
        } else if (number >= 10) {
            sb.Append(number switch {
                >= 90 => "XC",
                >= 80 => "LXXX",
                >= 70 => "LXX",
                >= 60 => "LX",
                >= 50 => "L",
                >= 40 => "XL",
                >= 30 => "XXX",
                >= 20 => "XX",
                _ => "X",
            });
            number %= 10;
        } else {

```