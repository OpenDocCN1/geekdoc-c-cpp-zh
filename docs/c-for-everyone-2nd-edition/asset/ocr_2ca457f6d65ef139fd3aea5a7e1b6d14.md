**R3.9** In a scheduling program, we want to check whether two appointments overlap. For simplicity, appointments start at a full hour, and we use military time (with hours 0–23). The following pseudocode describes an algorithm that determines whether the appointment with start time **start1** and end time **end1** overlaps with the appointment with start time **start2** and end time **end2**.

```
```text
If start1 > start2
    s = start1
Else
    s = start2
If end1 < end2
    e = end1
Else
    e = end2
If s < e
    The appointments overlap.
Else
    The appointments don’t overlap.
```
```

Trace this algorithm with an appointment from 10–12 and one from 11–13, then with an appointment from 10–11 and one from 12–13.

**R3.10** Draw a flow chart for the algorithm in Exercise R3.9.

**R3.11** Draw a flow chart for the algorithm in Exercise P3.12.

**R3.12** Draw a flow chart for the algorithm in Exercise P3.13.

**R3.13** Develop a set of test cases for the algorithm in Exercise R3.9.

**R3.14** Develop a set of test cases for the algorithm in Exercise P3.13.

**R3.15** Write pseudocode for a program that prompts the user for a month and day and prints out whether it is one of the following four holidays:

+   - New Year’s Day (January 1)
+   - Independence Day (July 4)
+   - Veterans Day (November 11)
+   - Christmas Day (December 25)

**R3.16** Write pseudocode for a program that assigns letter grades for a quiz, according to the following table:

| Score | Grade |
|---|---|
| 90–100 | A |
| 80–89 | B |
| 70–79 | C |
| 60–69 | D |
| < 60 | F |

**R3.17** Explain how the lexicographic ordering of strings in C++ differs from the ordering of words in a dictionary or telephone book. *Hint:* Consider strings such as IBM, wiley.com, Century 21, and While-U-Wait.

**R3.18** Of the following pairs of strings, which comes first in lexicographic order?

+   a. "Tom", "Dick"
+   b. "Tom", "Tomato"
+   c. "Church", "Churchill"