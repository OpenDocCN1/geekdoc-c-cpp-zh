```
```csharp
using System;
using System.Text.RegularExpressions;
namespace RegularExpApp {
    class MyProgram {
        static void Main(string[] args) {
            string text = "Hi  learner  ";
            string pattern = "\\s+";
            string substitute = " ";
            Regex r = new Regex(pattern);
            string output = r.Replace(text, substitute);
            Console.WriteLine("The input string is: {0}", text);
            Console.WriteLine("The string after replacement is: {0}", output);
            Console.ReadKey();
        }
    }
}
```
```

The code returns the following:

![](bbox=[0.036, 0.483, 0.942, 0.604])

What we are doing in the code is that we are replacing the extra white space. There is a big space between “Hi” and “learner”. The extra one has been replaced or removed.