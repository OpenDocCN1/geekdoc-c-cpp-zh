Sample Test Data To test this analysis, we select a set of values, for example 23, 15, and 12 and work through the steps of the algorithm of Figure 1.8.

| STEP | 1 | 2 | 3 | 2 | 3 | 2 | 4 | 5 |
|---|---|---|---|---|---|---|---|---|n| Count | 0 | 0 | 1 | 2 | 2 | 3 | 3 | 3 |
| Total | 0 | 0 | 23 | 23 | 38 | 50 | 50 | 50 | 50 |
| Data | - | 23 | 23 | 15 | 15 | 12 | 12 | - | - |
| Average | - | - | - | - | - | - | - | 16.67 | - |
| Output | - | - | - | - | - | - | - | - | 16.67 |

The algorithm is correct with this ordinary data. However, using extreme data may uncover errors—for example, if there are no positive data values.

| STEP | 1 | 2 | 4 | 5 |
|---|---|---|---|---|n| Total | 0 | 0 | 0 | - |
| Count | 0 | 0 | 0 | - |
| Data | - | - | 0/0 | - |
| Average | - | - | - | - |
| Output | - | - | - | - |

This is a logical and computational error. This situation could be detected by checking the value of the count before computing the average, as shown in Figure 1.9.

At this stage of the design process, working with both words and a variety of diagrams provides more insight into the solution than either method would by itself. Errors found when working with the diagrams can be used to correct the specifications, which in turn leads to changes in the diagrams. This feedback and correction process should be repeated until the designer is satisfied that the solution is feasible with available computer resources. Any errors not found during the design phase can be very expensive to correct later on.

Structure Chart Structure charts were introduced in Section 1.2.2 as a way to show modularity. Since each step in an algorithm is a simple module, they can be used to represent an algorithm. The steps in Figure 1.10 are numbered for easy reference. The structure chart in Figure 1.10 corresponds to the levels of