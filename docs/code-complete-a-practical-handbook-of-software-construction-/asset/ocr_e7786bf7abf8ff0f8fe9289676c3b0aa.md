# Code Reading

Code reading is an alternative to inspections and walk-throughs. In code reading, you read source code and look for errors. You also comment on qualitative aspects of the code, such as its design, style, readability, maintainability, and efficiency.

![](bbox=[0.09, 0.19, 0.15, 0.27])

A study at NASA’s Software Engineering Laboratory found that code reading detected about 3.3 defects per hour of effort. Testing detected about 1.8 errors per hour (Card 1987). Code reading also found 20 to 60 percent more errors over the life of the project than the various kinds of testing did.

Like the idea of a walk-through, the concept of code reading is loosely defined. A code reading usually involves two or more people reading code independently and then meeting with the author of the code to discuss it. Here’s how code reading goes:

+   - In preparation for the meeting, the author of the code hands out source listings to the code readers. The listings are from 1000 to 10,000 lines of code; 4000 lines is typical.
+   - Two or more people read the code. Use at least two people to encourage competition between the reviewers. If you use more than two, measure everyone’s contribution so that you know how much the extra people contribute.
+   - Reviewers read the code independently. Estimate a rate of about 1000 lines a day.
+   - When the reviewers have finished reading the code, the code-reading meeting is hosted by the author of the code. The meeting lasts one or two hours and focuses on problems discovered by the code readers. No one makes any attempt to walk through the code line by line. The meeting is not even strictly necessary.
+   - The author of the code fixes the problems identified by the reviewers.

![](bbox=[0.09, 0.67, 0.16, 0.75])

The difference between code reading on the one hand and inspections and walk-throughs on the other is that code reading focuses more on individual review of the code than on the meeting. The result is that each reviewer’s time is focused on finding problems in the code. Less time is spent in meetings in which each person contributes only part of the time and in which a substantial amount of the effort goes into moderating group dynamics. Less time is spent delaying meetings until each person in the group can meet for two hours. Code readings are especially valuable in situations in which reviewers are geographically dispersed.

![](bbox=[0.09, 0.83, 0.16, 0.91])

A study of 13 reviews at AT&T found that the importance of the review meeting itself was overrated; 90 percent of the defects were found in preparation for the review meeting, and only about 10 percent were found during the review itself (Votta 1991, Glass 1999).