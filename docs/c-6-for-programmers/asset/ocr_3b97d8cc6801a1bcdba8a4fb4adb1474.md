```
// return average of grades
return total / gradeCount;
}

// output bar chart displaying overall grade distribution
public void OutputBarChart()
{
    Console.WriteLine("Overall grade distribution:");

    // stores frequency of grades in each range of 10 grades
    var frequency = new int[11];

    // for each grade in GradeBook, increment the appropriate frequency
    foreach (var grade in grades)
    {
        ++frequency[grade / 10];
    }

    // for each grade frequency, display bar in chart
    for (var count = 0; count < frequency.Length; ++count)
    {
        // output bar label ("00-09: ", ..., "90-99: ", "100: ")
        if (count == 10)
        {
            Console.Write(" 100: ");
        }
        else
        {
            Console.Write($"{count * 10:D2}-{count * 10 + 9:D2}: ");
        }

        // display bar of asterisks
        for (var stars = 0; stars < frequency[count]; ++stars)
        {
            Console.Write("*");
        }

        Console.WriteLine(); // start a new line of output
    }
}

// output the contents of the grades array
public void OutputGrades()
{
    Console.WriteLine("The grades are:\n");
    Console.Write(" "); // align column heads

    // create a column heading for each of the tests
    for (var test = 0; test < grades.GetLength(1); ++test)
    {
        Console.Write($"Test {test + 1} ");
    }
}
```