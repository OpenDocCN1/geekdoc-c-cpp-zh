![](bbox=[0.176, 0.095, 0.895, 0.271])

Figure 13-2 IntelliSense display

One of the `static` methods of the `File class` is `Exists( )`. Prior to writing program statements that access data in a file, you should always check to make sure the file is available. Example 13-1 illustrates invoking this method and several other methods that return information about the file.

# **Example 13-1**

```
```csharp
/* DirectoryStructure.cs
   Illustrates using File and Directory utilities.
*/
using System;
using System.IO;
class DirectoryStructure
{
   public static void Main( )
   {
      string fileName = "BirdOfParadise.jpg";

      if (File.Exists(fileName))
      {
         Console.WriteLine("FileName: {0}", fileName);
         Console.WriteLine("Attributes: {0}",
                           File.GetAttributes(fileName));
         Console.WriteLine("Created: {0}",
                           File.GetCreationTime(fileName) );
         Console.WriteLine("Last Accessed: {0}",
                           File.GetLastAccessTime(fileName));
```
```