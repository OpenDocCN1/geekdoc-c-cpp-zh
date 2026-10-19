# 22.4 Typical Errors

This section is dedicated to the proposition that you can test best when you know as much as possible about your enemy: errors.

# Which Classes Contain the Most Errors?

![](bbox=[0.12, 0.25, 0.22, 0.32])

It’s natural to assume that defects are distributed evenly throughout your source code. If you have an average of 10 defects per 1000 lines of code, you might assume that you’ll have one defect in a class that contains 100 lines of code. This is a natural assumption, but it’s wrong.

Capers Jones reported that a focused quality-improvement program at IBM identified 31 of 425 classes in the IMS system as error-prone. The 31 classes were repaired or completely redeveloped, and, in less than a year, customer-reported defects against IMS were reduced ten to one. Total maintenance costs were reduced by about 45 per cent. Customer satisfaction improved from “unacceptable” to “good” (Jones 2000).

Most errors tend to be concentrated in a few highly defective routines. Here is the general relationship between errors and code:

![](bbox=[0.12, 0.5, 0.22, 0.57])

+   - Eighty percent of the errors are found in 20 percent of a project’s classes or routines (Endres 1975, Gremillion 1984, Boehm 1987b, Shull et al 2002).
+   - Fifty percent of the errors are found in 5 percent of a project’s classes (Jones 2000).

These relationships might not seem so important until you recognize a few corollaries. First, 20% of a project’s routines contribute 80% of the cost of development (Boehm 1987b). That doesn’t necessarily mean that the 20% that cost the most are the same as the 20% with the most defects, but it’s pretty suggestive.

![](bbox=[0.12, 0.72, 0.22, 0.79])

Second, regardless of the exact proportion of the cost contributed by highly defective routines, highly defective routines are extremely expensive. In a classic study in the 1960s, IBM performed an analysis of its OS/360 operating system and found that errors were not distributed evenly across all routines but were concentrated into a few. Those error-prone routines were found to be “the most expensive entities in programming” (Jones 1986a). They contained as many as 50 defects per 1000 lines of code, and fixing them often cost 10 times what it took to develop the whole system. (The costs included customer support and in-the-field maintenance.)