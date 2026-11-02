```
/**
Converts a letter grade to a number.
@param grade a letter grade (A+, A, A-,..., D-, F)
@return the equivalent number grade
*/
double grade_to_number(string grade)
{
    double result = 0;
    string first = grade.substr(0, 1);
    if (first == "A") { result = 4; }
    else if (first == "B") { result = 3; }
    else if (first == "C") { result = 2; }
    else if (first == "D") { result = 1; }
    if (grade.length() > 1)
    {
        if (grade.substr(1, 1) == "+")
        {
            result = result + 0.3;
        }
        else
        {
            result = result - 0.3;
        }
    }
    return result;
}
```

# Step 3 Convert number grade to letter

How do we do the opposite conversion? Here, the challenge is that we need to convert to the nearest letter grade. For example, suppose x is 2.9. This value is closer to a B (2.3) than to a B- (2.7). When a value is exactly in the middle between two letter grade values, we give the higher grade. For example, 2.85 is rounded up to a B, and 3.15 is rounded up to a B+ (3.3). That is, any grade that is at least 2.85 but less than 3.15 is a B. We can make a function with 13 branches, one for each valid letter grade.

```
/**
Converts a number to the nearest letter grade.
@param x a number between 0 and 4.3
@return the nearest letter grade
*/
string number_to_grade(double x)
{
    if (x >= 4.15) { return "A+"; }
    if (x >= 3.85) { return "A"; }
    if (x >= 3.5) { return "A-"; }
    if (x >= 3.15) { return "B+"; }
    if (x >= 2.85) { return "B"; }
    if (x >= 2.5) { return "B-"; }
    if (x >= 2.15) { return "C+"; }
    if (x >= 1.85) { return "C"; }
    if (x >= 1.5) { return "C-"; }
    if (x >= 1.15) { return "D+"; }
    if (x >= 0.85) { return "D"; }
    if (x >= 0.5) { return "D-"; }
    return "F";
}
```

Exercise P5.5 suggests an alternate approach.