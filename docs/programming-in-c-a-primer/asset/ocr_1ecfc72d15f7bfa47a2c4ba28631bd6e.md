```
getresult = Console.ReadLine();
if (getresult == "y")
{
    Console.WriteLine("Removing 2nd Student details");
    Console.WriteLine("________________________");
    arrlists.Remove(studname2);
    arrlists.Remove(classname2);
    arrlists.Remove(rollno2);
    Console.WriteLine("Current Capcity of the arraylist is now =" + arrlists.Capacity);
    Console.WriteLine("Arraylist is having elements=" + arrlists.Count);
    Console.Write("The elements of Arraylist are now:-");
    for (int m = 0; m < arrlists.Count; m++)
    {
        Console.Write(arrlists[m] + " ");
    }
    Console.WriteLine("\n");
}
else
{
    Console.WriteLine("\n");
    Console.WriteLine("Changing elements");
    Console.WriteLine("________________________");
    arrlists[0] = studname3.ToString();
    arrlists[1] = classname3;
    arrlists[2] = rollno3;
    arrlists[6] = studname1;
    arrlists[7] = classname1;
    arrlists[8] = rollno1;
    Console.Write("Now the elements of the ArrayList are : ");
    for (int m = 0; m < arrlists.Count; m++)
    {
        Console.Write(arrlists[m] + " ");
    }
    Console.WriteLine("\n");
}
}
```

Remarks With the use of the C# application created by Siddharth, the administrative staff of B.G International School will be able to save time in entering the details such as names and classes of students studying in different classes.