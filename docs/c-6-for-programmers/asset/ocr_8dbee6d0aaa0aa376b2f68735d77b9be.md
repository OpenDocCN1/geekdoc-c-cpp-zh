This is a typical array-processing app (Fig. 8.9). We wish to summarize the number of responses of each type (that is, 1–5). Array responses (lines 10–11) is a 20-element integer array containing the students' survey responses. The last value in the array is intentionally an incorrect response (14). When a C# program executes, the runtime checks array element indices for validity—all indices must be greater than or equal to 0 and less than the length of the array. Any attempt to access an element outside that range of indices results in a runtime error known as an IndexOutOfRangeException. At the end of this section, we'll discuss the invalid response, demonstrate array bounds checking and introduce C#'s exception-handling mechanism, which can be used to detect and handle an IndexOutOfRangeException.

```
```csharp
 1   // Fig. 8.9: StudentPoll.cs
 2   // Poll analysis app.
 3   using System;
 4
 5   class StudentPoll
 6   {
 7      static void Main()
 8      {
 9         // student response array (more typically, input at runtime)
10         int[] responses = {1, 2, 5, 4, 3, 5, 2, 1, 3, 3, 1, 4, 3, 3, 3,
11            2, 3, 3, 2, 14};
12         var frequency = new int[6]; // array of frequency counters
13
14         // for each answer, select responses element and use that value
15         // as frequency index to determine element to increment
16         for (var answer = 0; answer < responses.Length; ++answer)
17         {
18            try
19            {
20               ++frequency[responses[answer]];
21            }
22            catch (IndexOutOfRangeException ex)
23            {
24               Console.WriteLine(ex.Message);
25               Console.WriteLine(
26                  $"   responses[{answer}] = {responses[answer]}\n");
27            }
28         }
29
30         Console.WriteLine($"{\"Rating\"}{\"Frequency\",10}");
31
32         // output each array element's value
33         for (var rating = 1; rating < frequency.Length; ++rating)
34         {
35            Console.WriteLine($"{rating,6}{frequency[rating],10}");
36         }
37      }
38   }
```
```

**Fig. 8.9** | Poll analysis app. (Part 1 of 2.)