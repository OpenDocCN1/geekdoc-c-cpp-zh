# Appendix B = Solutions to Exercises 495

```
// See if i is a Carmichael number.
If (IsCarmichael(i)) Then
    <Output i and its prime factors>
End If
Next i
GenerateCarmichaelNumbers

Return true if the number is a Carmichael number.
Boolean: IsCarmichael(Integer: number)
// Check all possible witnesses.
For i = 1 to number - 1
    If (GCD(number, i) == 1) Then
        // Use fast exponentiation to calculate
        i ^ (number-1) mod number>
        Integer: result = Exponentiate(i, number - 1, number)

// If we find a Fermat witness,
    // this is not a Carmichael number.
If (result != 1) Then Return false
End If
Next i
```

// They're all a bunch of liars!
// This is a Carmichael number.
Return true
IsCarmichael

You can download the CarmichaelNumbers example program from the book’s website to see a C# implementation of this algorithm.

+   15. Suppose you use the value of the function at the rectangle's midpoint for the rectangle's height. Then, if the function is increasing, the left part of the rectangle is too short, and the right part is too tall, so the error in two pieces cancels out, to some extent. Similarly, if the function is decreasing, the left part of the rectangle is too short, and the right part is too tall, so partially cancel out. This reduces the total error considerably without increasing the number of rectangles.

This method won’t help (may even hurt) if the curve has a local minimum or maximum near the middle of a rectangle. In those cases the errors on the left and right sides of the curve will add up and give a larger total error.

Figure-4 shows the MidpointRectangleRule example program, which is available for download on the book’s website, when you compare the result to the one shown in Figure 2-2, you'll see that the midpoint reduced the total error from about -6.5% to 0.2%, roughly 1/30th of the error, without changing the number of rectangles.