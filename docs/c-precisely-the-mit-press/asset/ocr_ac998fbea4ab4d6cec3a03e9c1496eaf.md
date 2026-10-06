# Example 4 Using Keywords as Identifier Names

This feature is provided for interoperability with other programming languages, in which class or public may be a perfectly legal name for a field or method; it should not be used in ordinary C# programming. Note that for non-keywords as i, the identifier @i is the same as the i.

```
class School {
    const int @class = 2004;
    const bool @public = true;
    String @delegate = "J. Smith ";
    public static int @double(int i) { return @i; }
}

School school = new School();
Console.WriteLine(school.delegate.Trim() + " " + School.class);
```

# Example 5 A One-Line Comment, a Delimited Comment, and Abuse of a Delimited Comment

```
class Comment {
// This is a one-line comment; it extends to the end of the line
/* This is a delimited comment
   extending over several lines.
   */
int /* * This delimited comment extends over part of a line /* x = 117;
}
```

# Example 6 Program Layout Style

```
class LayoutExample {
    int j;

    LayoutExample(int j) {
        this.j = j;
    }

    int Sum(int b) {
        if (j > 0) {
            return j + b;
        } else if (j < 0) {
            int res = -j + b;
            return res * 117;
        } else { // j == 0 {
            int sum = 0;
            for (int i=0; i<10; i++) {
                sum += (b - i) * (b - i);
            }
            return sum;
        }
    }
}
```