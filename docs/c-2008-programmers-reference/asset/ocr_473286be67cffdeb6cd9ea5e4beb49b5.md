(continued)

```
```csharp
//---begin to read asynchronously---
IAsyncResult result =
    fs_in.BeginRead(buffer, 0, BUFFER_SIZE,
        new AsyncCallback(readCompleted), null);

//---continue with the execution---
for (int i = 0; i < 100; i++)
{
    Console.WriteLine("Continuing with the execution...{0}", i);
    System.Threading.Thread.Sleep(250);
}
catch (Exception ex)
{
    Console.WriteLine(ex.ToString());
}
Console.ReadLine();
```
```

```
```csharp
//---when a block of data is read---
static void readCompleted(IAsyncResult result)
{
    //---simulate slow reading---
    System.Threading.Thread.Sleep(500);

    //---reads the data---
    int bytesRead = fs_in.EndRead(result);

    //---writes to another file---
    fs_out.Write(buffer, 0, bytesRead);

    if (bytesRead > 0)
    {
        //---continue reading---
        result =
            fs_in.BeginRead(buffer, 0, BUFFER_SIZE,
                new AsyncCallback(readCompleted), null);
    }
    else
    {
        //---reading is done!---
        fs_in.Dispose();
        fs_out.Dispose();
        fs_in.Close();
        fs_out.Close();
        Console.WriteLine("File copy done!");
    }
}
```
```