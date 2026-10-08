# 8.5 Using Arrays to Analyze Survey Results; Intro to Exception Handling 353

# 8.5 Using Arrays to Analyze Survey Results; Intro to Exception Handling

Our next example uses arrays to summarize data collected in a survey. Consider the following problem statement:

+   - Twenty students were asked to rate on a scale of 1 to 5 the quality of the food in the student cafeteria, with 1 being 'awful' and 5 being 'excellent.' Place the 20 responses in an integer array and determine the frequency of each rating.

This is a typical array-processing app (Fig. 8). We wish to summarize the number of responses of each type (that is, 1–5). Array responses (lines 10–11) are a 20-element integer array containing the students' responses. The last value is intentionally an incorrect response (14). As C executes, the runtime checks array elements for validity—all indices must be greater than 0 and less than the length of the array. Any attempt to access an element outside that range of indices results in a runtime error known as IndexOutOfRangeException. At the end of this section, we'll discuss the invalid response, demonstrate array checking and introduce C#'s exception-handling mechanism, which can be used to detect and handle IndexOutOfRangeException.

```
// Fig. 8.9: StudentPoll.cs
// Poll analysis app.
using System;
class StudentPoll {
static void Main() {
// student response array (more typically, input at runtime)
int[] responses = {1, 2, 5, 4, 3, 5, 2, 1, 3, 3, 1, 4, 3, 3, 2, 3, 2, 14};
var frequency = new int[6]; // array of frequency counters

// for each answer, select responses element and use that value
// as index to determine element to increment
for (var answer = 0; answer < responses.Length; answer++) {
try {
++frequency[responses[answer]];
} catch (IndexOutOfRangeException ex) {
Console.WriteLine(ex.Message);
Console.WriteLine($" {responses[answer]} = {responses[answer]}\n");
}
}
```

Fig. 8.9 | Poll analysis app. (Part I of 2).