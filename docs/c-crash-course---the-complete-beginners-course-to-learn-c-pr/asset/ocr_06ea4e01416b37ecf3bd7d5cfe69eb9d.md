```
for (int i = 0; i <= 20; i++)
{
    Console.Write(F.ReadByte() + " ");
}
F.Close();
```

Notice when we used the same exact code as in the previous sections, but we changed the file mode when we opened the file. Instead of telling the compiler to open or create the file, we told it to open the file to append information to it. If the file doesn't exist, the following code will cause an error, you'll need to make sure that the F variable isn't null. We assume in this code that the test.txt file exists, so we don't need to check that the file variable is null.

Instead of creating a file with the values of 1 to 20, we append the data to the file. So if the file already contains data, these values will be written after the current data. This includes cases where you already wrote the same data to the file.

# Deleting a File

You won't only need to create and read and write to a file. There are times you'll need to delete a file as well. Luckily, the .NET framework makes it just as easy to delete a file as it does to create and work with file data.

It's even easier to delete a file than perform the other processes. You use a different class library to delete a file. The FileStream library is strictly to read and write to files, but the class is a static class that does short, quick tasks to complete a process. In this case, we want to delete a file, which doesn't need any elaborate code.

Let's take a look at what the code looks like to delete a file from the hard drive.

```
if(File.Exists(@"C:\test.txt")
{
    File.Delete(@"C:\test.txt");
}
```

In the above code, we first test to see if the file exists before we actually attempt to delete it. We specify a location, which we didn't do in the previous sections. We use the static method "Exists" to first test if the file actually does exist. If it does, we move into the if statement block of code. We use another static method in the File class called Delete. Delete is the method that does the actual deletion of the file.

Reading, writing, and deleting files are the three main functions you'll need to know when you work with files. Of course, you still need permissions to work with files. The