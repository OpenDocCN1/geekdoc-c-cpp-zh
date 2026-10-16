called the Exist method. If you attempted to read from a file that isn’t there, you can expect to see errors.

# Quick Primer

+   - Reading and writing to a file is sometimes known as file input and output but is more often called file I/O.
+   - File I/O is not difficult to do in C#, but not as complicated as other languages.
+   - Everything you do with file I/O will always begin with the class called File.
+   - If you want to write multiple lines to a file at the same time, use File.WriteAllLines( string filePath, string[] lines);.
+   - If you want to write the entire contents of a file out at the same time, you would use File.WriteAllText(string filePath, string allText);.
+   - When you do file I/O, there is a good chance that your data will need to be turned into a format that fits with the output methods; the text would then need to be parsed back in allowing your objects to be reconstructed. In simpler terms, there is much more to file writing that just putting the data into the file – it must also be in the correct format to work properly.
+   - Text-based and binary files are read and written in different ways. With the binary files, we can read and write a little at a time whereas, with the text-based files, it is all at once. Whichever way you do this, you always begin with File.OpenRead or with File.OpenWrite. The FileStream that is returned is wrapped in either a TextReader or TextWriter or a BinaryReader or BinaryWriter, depending on what you are doing. Then you can do all the reading and writing you want; when you have finished with the writing, always call the Flush method for the writer and call the Close method for the reader or the writer.

# What's Next?

File I/O is incredibly powerful and it is one of the most important parts of programming that you can learn to do. Almost every program you come across will require this in one form or another.