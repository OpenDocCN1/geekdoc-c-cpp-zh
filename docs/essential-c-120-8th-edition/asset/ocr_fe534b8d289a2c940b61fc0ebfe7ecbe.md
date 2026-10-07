# Chapter 5: Parameters = Methods

```
HttpClient client = new();
byte[] response =
    client.GetByteArrayAsync(urlString).Result;
    client.Dispose();
    File.WriteAllBytes(filename, response);
    Console.WriteLine($"Downloaded {filename}' from '{n        urlString}\');
    result = 0;
}
    return result;
```

# OUTPUT 5.3

> > Downloader
ERROR: You must specify the URL and the file name
Usage: Downloader.exe <TargetFileName>
>Downloader https://IntelliText.com Index.html
Downloaded 'Index.html' from 'https://IntelliText.com'.

If you were successful in calculating the target filename, you would use to save the downloaded file. Otherwise, you would display the help text. The Main() method, but if it is used, the program can return an exit code to a caller (such as a script or a batch file). By convention, a return other than zero indicates an error.

Although all command-line arguments can be passed to Main() via an array of strings, it is convenient to access the arguments from inside a method other than Main(). The System.Environment.GetCommandLineArgs() method returns the command-line arguments in the same form that Main(string[]) args passes the arguments into the Main method except that the first item in the array is the executable file.

To download the file, Listing 5.16 uses a System.Http.HttpClient object but only specified HttpClient—its namespace is imported by the ImplicitUsings element in the .csproj file.