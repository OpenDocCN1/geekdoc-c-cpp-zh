the guidance software produced an inaccurate calculation of the time since system start-up due to accumulated roundoff errors that result from inexact binary representations of real numbers. And this time calculation was a key factor in determining the exact location of the incoming missile. The sad epilogue is that corrected software arrived in Dharan on February 26, the next day.

These are but a few examples of program errors that are more than just a nuisance and can lead to very serious and even tragic results. In such cases, careful software design, coding, and extensive and thorough testing are mandatory. In safety-critical situations where errors cannot be tolerated, relying on the results of test runs may not be sufficient because *testing can show only the presence of errors, not their absence.* It may be necessary to give a deductive proof that the program is correct and that it will always produce the correct results (assuming no system malfunction).

# 2.2.5 Maintenance

In contrast to student programs that are often run once or twice and then discarded, real-world programs may represent a significant investment of a company’s resources and be used for many years, during which time new features or enhancements may be added to upgrade the program. To illustrate, users of the program in Example 2.2 might find it more useful to be able to choose between Celsius-to-Fahrenheit and Fahrenheit-to-Celsius conversions and perhaps to add the Kelvin scale also. Because a program that offers these alternatives uses more advanced programming features, we will defer it until the next chapter.

# CHAPTER SUMMARY

Key Terms

| #include | debugger |
| algorithm | debugging |
| behavior | design |
| C++ | generalization |
| cin | input (>>) |
| class | library |
| coding | logic error |
| comment (/*, */, //) | main function |
| compiler | maintenance |
| compiler directive | namespace |
| cout | object-centered design (OCD) |
| curly braces ({ and }) | object-oriented design |