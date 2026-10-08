```
        writer.WriteLine("Line 1");
        writer.WriteLine("Line 2");
      }
      
      File.Copy(tempFile, Path.GetTempFileName());
      File.Delete(tempFile);
    }
    catch (IOException e)
    {
      Console.WriteLine("An error occurred: {0}", e.Message);
    }
  }
}
```

# ## Working with the Directory and File Classes

By following these steps, you learn how to work with the Directory and File classes. If you closed Visual Studio, repeat the previous exercise first. Be sure to keep Visual Studio open at the end of this exercise because you will use this application later.

+   1. Modify the call to `EnumerateDirectories` to call the method on Directory of the same name, enumerating over the C:\Windows\Web\Wallpaper directory. Use the following code to retrieve this folder path:

```
Path.Combine(
  Environment.GetFolderPath(Environment.SpecialFolder.Windows),
  "Web",
  "Wallpaper")
```

+   2. Modify the nested foreach statement to call `Directory.EnumerateFiles`. Because this returns a path string rather than a FileInfo, you also need to modify the statement that prints the filename and creation time to get the file-name from the resulting path string and use the appropriate static method on the File class to retrieve the creation date and time.

+   3. Run the application using Ctrl+F5. The output should match the output generated from step 6 of the previous exercise.

# ## Reading and Writing Data

Working with the data contained in files (by either reading or writing) uses streams, represented by the Stream class. All stream-based classes provided by the .NET Framework derive from this class. The commonly used members of the Stream class are shown in Table 13.7.