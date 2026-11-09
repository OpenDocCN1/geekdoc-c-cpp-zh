# FOR Loop Example 3 – Nested Loops

In the final example, we use FOR loops to create a star pattern.
So, we create a 2<sup>nd</sup> button labelled ‘Print Star Loop’ which runs **starloop()** on clicking. In the function, again, looplength has the value of the loop we enter in the form.
So, first, we create a FOR loop that goes from 1 to looplength. The variable i holds the count value of the loop and increases by 1 each time.
Then, we create another FOR loop within that goes from 1 to i. The second FOR loop prints the star(“*”) i times.
So, for example, if you’re going through the first loop for the 5<sup>th</sup> time, i=5.
The second loop prints * from 1 to 5 (i.e. 5 times).
In the example, below, we print the star loop for a looplength of 23.