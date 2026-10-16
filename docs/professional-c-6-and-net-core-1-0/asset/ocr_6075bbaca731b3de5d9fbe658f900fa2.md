```
public class Program
{
    public static void Main()
    {
        Write("Please type in the name of the file" +
            "containing the names of the people to be cold called
>");
        string fileName = ReadLine();
        ColdCallFileReaderLoop1(fileName);
        WriteLine();
        ReadLine();
    }

    public static ColdCallFileReaderLoop1(string filename)
    {
        var peopleToRing = new ColdCallFileReader();

        try
        {
            peopleToRing.Open(fileName);
            for (int i = 0; i < peopleToRing.NPeopleToRing; i++)
            {
                peopleToRing.ProcessNextPerson();
            }
            WriteLine("All callers processed correctly");
        }
        catch(FileNotFoundException)
        {
            WriteLine($"The file {fileName} does not exist");
        }
        catch(ColdCallFileFormatException ex)
        {
            WriteLine($"The file {fileName} appears to have been corrupted");
            WriteLine($"Details of problem are: {ex.Message}");
            if (ex.InnerException != null)
            {
                WriteLine($"Inner exception was: {ex.InnerException.Message}");
            }
        }
        catch(Exception ex)
        {
            WriteLine($"Exception occurred:\n{ex.Message}");
        }
        finally
        {
            peopleToRing.Dispose();
        }
    }
}
```

This code is a little more than just a loop to process people from the file. You start by asking the user for the name of the file. Then you instantiate an object of a class called ColdCallFileReader, which is defined shortly. The ColdCallFileReader class is the class that handles the file reading. Notice that you do this outside the initial try block—that’s because the variables that you instantiate here need to be available in the subsequent catch and finally blocks, and if you declare them inside the try block they would go out of scope at the closing curly brace of the try block, where the compiler would complain about