39. Modify the program developed in Problem 37 so that the user can enter a number of acres and the program will determine how many years are required for the number of acres to be completely reforested.

# Critical Path Analysis.

A critical path analysis is a technique used to determine the time schedule for a project. This information is important in the planning stages before a project is begun, and it is also useful to evaluate the progress of a project that is partially completed. One method for this analysis starts by dividing a project into sequential events and then dividing each event into various tasks. Although one event must be completed before the next one is started, various tasks within an event can occur simultaneously. The time it takes to complete an event, therefore, depends on the number of days required to finish its longest task. Similarly, the total time it takes to finish a project is the sum of time it takes to finish each event.

Assume that the critical path information for a major construction project has been stored in a data file. Each line of the data file contains an event number, a task number, and the number of days required to complete the task. The data have been stored such that all the task data for the first event are followed by all the task data for the second event, and so on. A typical set of data is shown in the following table.

| Event | Task | Number of Days |
| :--- | :--- | :--- |
| 1 | 15 | 3 |
| 1 | 27 | 6 |
| 1 | 36 | 4 |
| 2 | 15 | 5 |
| 3 | 18 | 4 |
| 3 | 26 | 1 |
| 4 | 15 | 2 |
| 4 | 26 | 7 |
| 4 | 27 | 7 |
| 5 | 16 | 4 |

40. Write a program to read the critical path information and to print a project completion timetable that lists each event number, the maximum number of days for a task within the event, and the total number of days for the project completion.

41. Write a program to read the critical path information and to print a report that lists the event number and task number for all tasks requiring more than five days.

42. Write a program to read the critical path information and to print a report that lists the number of each event and a count of the number of tasks within the event.

# Weather Balloons.

Weather balloons are used to gather temperature and pressure data at various altitudes in the atmosphere. The balloon rises because the density of the helium inside the balloon is less than the density of the surrounding air outside the balloon. As the balloon rises, the surrounding air becomes less dense, and thus the balloon's ascent slows until it