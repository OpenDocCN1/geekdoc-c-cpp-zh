4. Click thread 2. Its activity level is Low. Change it to Maximum.

5. Change the process affinity mask to a single logical processor. To do so, open the Process menu and choose Affinity. (It doesn't matter which processor.) Alternatively, use User Manager to manage the change. The screen should look something like this:

![](bbox=[0.196, 0.168, 0.722, 0.303])

6. Start the Performance Monitor tool.

7. Click the Add Counter toolbar button or press Ctrl+I to open the Add Counters dialog box.

8. Select the Thread object and select the Priority Current counter.

9. In the Instances box, type CPUSTRES and click Search.

10. Select threads 1 and 2 (thread 0 is the GUI thread), click the Add button, and click OK.

11. Change the vertical scale to 16 for both counters.

12. Because Performance Monitor refreshes once per second, you may see the priority boosts. To help with that, press Ctrl+F to freeze the display. Then force updates to occur more frequently by pressing and holding Ctrl+U. With some luck, you may see a priority boost for the lower-priority thread to level 15 like so:

![](bbox=[0.196, 0.588, 0.722, 0.873])

13. Exit Performance Monitor and CPU Stress.