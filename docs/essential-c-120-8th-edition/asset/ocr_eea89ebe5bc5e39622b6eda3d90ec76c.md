# Basic Error Handling with Exceptions 287

# Additional Parameter Validation

There are obviously a myriad of other type constraints that a method may have on its parameters. Perhaps a string argument should not be an empty string, should not be comprised only of whitespace, or must have "HTTPS" as a prefix. Listing 5.34 displays the full DownloadSSL() method, demonstrating this validation.

Listing 5.34: Custom Parameter Validation

```
public class Program {
    public static void main(string[] args) {
        int result = 0;
        if(args.Length != 2 ) {
            // Exactly two arguments must be specified; give an error
            Console.WriteLine("ERROR: You must specify " + URL and the file name");
            Console.WriteLine("Usage: Downloader.exe <URL> <TargetFileName>");
            result = 1;
        } else {
            DownloadSSL(args[0], args[1]);
            return result;
        }
    }

    private static void DownloadSSL(string httpsUrl, string fileName) {
        #if !NET7_0_OR_GREATER
        httpsUrl = httpsUrl?.Trim() ??
            throw new ArgumentNullException(nameof(httpsUrl));
        fileName = fileName ??
            throw new ArgumentNullException(nameof(fileName));
        if (fileName.Trim().Length == 0) {
            throw new ArgumentException("${nameof(fileName)} cannot be empty or only whitespace");
        }
        #else
        ArgumentException.IfNullOrEmpty(httpsUrl = httpsUrl?.Trim()!);
        ArgumentException.IfNullOrEmpty(fileName = fileName?.Trim()!);
    }
}
```