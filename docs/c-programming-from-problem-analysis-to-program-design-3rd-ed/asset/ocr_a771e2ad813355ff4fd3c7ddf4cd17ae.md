```
avg = total / score.Length;                         //Line 6
Console.WriteLine( );
Console.WriteLine("Average: {0}",
        avg);

// Output is the array
// element and how far the value is
// from the mean (absolute value).
Console.WriteLine( );
Console.WriteLine("Score\tDist. from Avg.");
for (int i = 0; i < score.Length; i++)
{
    distance = Math.Abs((avg - score[i]));          //Line 7
    Console.WriteLine("{0}\t{1}",
            score[i], distance);                     //Line 8
}
}
}
```

In Example 7-6 on Line 1, the array is declared and space is allocated for 10 scores. Line 2 uses the Length property of the System.Array class as the expression for the loop control variable (i < score.Length). This loop is used to accumulate scores. score.Length returns 10; thus, 10 iterations of the loop are performed. The property score.Length is also used as the divisor representing the number of scores in the calculation of avg on Line 6.

The loop control variable, i, is displayed with 1 added to its value on Line 3. Here, it is used as part of the prompt to the user concerning which score to enter. Instead of first displaying “Enter Score0”, the display reads “Enter Score1”. The last prompt displays “Enter Score10”. Adding 1 to the index produces less confusing output for the user who does not realize that the first score is associated with location zero.

The statement labeled Line 4, also part of the loop body, assigns the converted integer to the array. Line 5 does another assignment statement when the array value is added to total. The distance from the average is found in line 7 by first subtracting the individual score from the average, which might yield a positive or negative value. Taking the absolute value (Math.Abs) ensures that the distance is positive.

Line 8, inside another loop, displays the contents of each element. The loop control variable serves as the index to the array, indicating which element to access. Figure 7-5 shows the output produced from one test run of Example 7-6.