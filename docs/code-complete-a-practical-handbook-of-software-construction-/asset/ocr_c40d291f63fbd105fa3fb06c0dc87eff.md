point in the project. Table 20-2 shows the percentages of defects detected by several common defect-detection techniques.

# Table 20-2  Defect-Detection Rates

| Removal Step | Lowest Rate | Modal Rate | Highest Rate |
|---|---:|---:|---:|
| Informal design reviews | 25% | 35% | 40% |
| Formal design inspections | 45% | 55% | 65% |
| Informal code reviews | 20% | 25% | 35% |
| Formal code inspections | 45% | 60% | 70% |
| Modeling or prototyping | 35% | 65% | 80% |
| Personal desk-checking of code | 20% | 40% | 60% |
| Unit test | 15% | 30% | 50% |
| New function (component) test | 20% | 30% | 35% |
| Integration test | 25% | 35% | 40% |
| Regression test | 15% | 25% | 30% |
| System test | 25% | 40% | 55% |
| Low-volume beta test (<10 sites) | 25% | 35% | 40% |
| High-volume beta test (>1,000 sites) | 60% | 75% | 85% |

> Source: Adapted from *Programming Productivity* (Jones 1986a), “Software Defect-Removal Efficiency” (Jones 1996), and “What We Have Learned About Fighting Defects” (Shull et al. 2002).

![](bbox=[0.136, 0.507, 0.208, 0.568])

The most interesting facts that this data reveals is that the modal rates don’t rise above 75 percent for any single technique and that the techniques average about 40 percent. Moreover, for the most common kinds of defect detection—unit testing and integration testing—the modal rates are only 30–35 percent. The typical organization uses a test-heavy defect-removal approach and achieves only about 85 percent defect-removal efficiency. Leading organizations use a wider variety of techniques and achieve defect-removal efficiencies of 95 percent or higher (Jones 2000).

The strong implication is that if project developers are striving for a higher defect-detection rate, they need to use a combination of techniques. A classic study by Glenford Myers confirmed this implication (1978b). Myers studied a group of programmers with a minimum of 7 and an average of 11 years of professional experience. Using a program with 15 known errors, he had each programmer look for errors by using one of these techniques:

+   - Execution testing against the specification
+   - Execution testing against the specification with the source code
+   - Walk-through/inspection using the specification and the source code