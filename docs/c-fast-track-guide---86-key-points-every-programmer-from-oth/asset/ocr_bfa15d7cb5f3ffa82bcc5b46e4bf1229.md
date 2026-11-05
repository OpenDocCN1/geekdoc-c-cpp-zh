System.IO.File.WriteAllText writes the entire string to the file. If the file already exists, it is overwritten.

System.IO.File.ReadAllText reads the entire file content as a single string.

These methods are useful for simple file operations without needing to manage streams manually.

Note that:

+   - File path can be absolute or relative.
+   - Exceptions (like IOException, UnauthorizedAccessException) may occur if the file cannot be accessed.
+   - Always handle exceptions in real applications for safety.
+   - Also, StreamReader and StreamWriter allow more control when reading or writing large files line-by-line.

# [Supplement]

+   - Files can also be written in binary format using File.WriteAllBytes.
+   - Use File.AppendText or File.AppendAllText if you want to add content to existing files.
+   - You can use Directory.Exists(path) to check for folders.
+   - File access may differ based on OS and permissions, especially between Windows and Linux.