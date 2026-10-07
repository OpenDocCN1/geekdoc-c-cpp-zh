# 248 Chapter 5: Parameters and Methods

5.17, the value of each variable that Main() uses when calling Combine() will be copied into the parameters of the Combine() method. Output 5.4 shows the results of this listing.

LISTING 5.17: Passing Variables by Value

```
public class Program {
    public static void Main() {
        // ...
        string fullName;
        string driveLetter = "C:";
        string folderPath = "Data";
        string fileName = "index.html";

        fullName = Combine(driveLetter, folderPath, fileName);

        Console.WriteLine(fullName);
        // ...
    }

    static string Combine(string driveLetter, string folderPath, string fileName) {
        string path;
        path = String.Format("{0}{1}{0}{2}{0}{0}{3}",
            Path.DirectorySeparatorChar,
            driveLetter, folderPath, fileName);
        return path;
    }
}
```

OUTPUT 5.4

C:\Users\Inigo\Data\index.html

Even if the Combine() method assigned null to driveLetter, folderPath, and fileName before returning, the corresponding variables within Main() will maintain their original values because the variables are copied when calling a method. When the call stack unwinds at the end of a call, the copied data is thrown away.