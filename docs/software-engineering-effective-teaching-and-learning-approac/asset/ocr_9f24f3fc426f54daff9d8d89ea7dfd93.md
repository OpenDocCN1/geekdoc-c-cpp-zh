# Elaboration of the Test Plan

Once the students understand the goals of the course and get familiarized with the system to test, they must start elaborating the test plan. This document is required to be formatted as a technical report, this point is the special interest because students are very close to finish their degree and need to be prepared for dealing with the document formatting standards used in the software development industry. This document must be realistic and include a schedule and milestones adjusted to the course length.

# Unit Testing

Unit testing is one of the core practices of XP and consists of taking each class of an object oriented software system and testing it in isolation. Students are encouraged to select a bottom-up testing approach, i.e. testing the classes of the system first and then testing the sum of its classes. On such an approach, integration testing becomes much easier. Teachers also encourage students to put special emphasis on unit testing due to the following reasons:

+   - Unit testing implicitly involves a sort of documentation that provides students with a better understanding of modules, requirements and API's.
+   - Good unit tests are fundamental when doing regression tests.

Since Java is the programming language selected for the course, the tool selected to assist the unit testing process can’t be other than JUnit. Many issues concerning test cases design and the right way to test an object in isolation need to be covered for an in-depth understanding of unit testing. In the following subsections we describe these issues in detail, providing some teaching recommendations obtained from our experience holding the course. However, note that some aspects, like test cases design, are not uniquely correlated with unit testing.

# Test Cases Design

The first step when doing unit testing is to design the test cases, black box and white box techniques are both suitable for this purpose. Black box consists of testing whether the output of a function

Figure 1. Diagram of the system to be tested and its environment

![](bbox=[0.24, 0.68, 0.73, 0.9])