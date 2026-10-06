# CHAPTER 14 Files and Streams

(continued)

file position by first subtracting 1 from the user's entry. The calculated record number is then multiplied by the size of each name in the file. For example, if each name is 10 bytes long, then the calculated starting position should be 0, 10, 20, 30, or some other method of the name size.

```
while(num == END)
{
    WriteLine("Starting " + num + ":\n    File.Seek(num - 1) * size, SeekOrigin.Begin);
```

+   2. Read and write the name at the calculated location. Then, in a nested loop, read and write all the remaining names until the end of the file.

```
name = reader.ReadLine();
WriteLine(" " + name);
while(name != null)
{
    name = reader.ReadLine();
    WriteLine(" " + name);
}
```

+   3. Finally, prompt the user for the next starting value for a new list, inform the user how to quit the application, and accept the next input value. Add a closing brace for the outer loop.

+   4. Close the StreamReader and File objects, and add closing braces for the method and the class.

```
reader.Close();
file.Close();
}
```

+   5. Save the file, and then compile and execute it. Figure 14-20 shows a typical execution during which the user displays three sets of names starting at a different point time.

(continues)