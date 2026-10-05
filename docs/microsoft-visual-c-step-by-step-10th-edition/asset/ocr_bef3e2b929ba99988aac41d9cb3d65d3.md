```
4, pixelWidth / 2));
Task.WaitAll(first, second);
..
```

+   9. On the **Debug** menu, select **Start Without Debugging** to build and run the application.

+   10. In the Graph Demo window, select **Plot Graph** and note the duration of the operation.

+   11. Repeat this step several times to get an average value. You should see that the application runs significantly quicker than it did previously. On my computer, the typical time dropped to 654 milliseconds—a reduction in time of approximately 45 percent.

In most cases, the time required to perform the calculations will be cut by nearly half. However, the application still has some single-threaded elements, such as the logic that actually displays the graph after the data has been generated. This is why the overall time is still more than half the time taken by the previous version of the application.

+   12. Stop the application and return to Visual Studio.

+   13. On the **Debug** menu, select **Relaunch Performance Profiler**. Performance Profiler starts using the performance settings specified earlier.

+   14. Select **Plot Graph** several times, waiting for a few seconds between selections. Note that the performance will have dropped slightly due to the effects of Performance Profiler.

+   15. Close the app and wait for Performance Profiler to generate the report.

In the CPU graph, you should see that the application uses more CPU resources than before. On my quad-core machine, the CPU peaked at approximately 50 percent each time I selected Plot Graph. This happens because the two tasks were run on separate cores, that the remaining cores were left unoccupied. If you have a dual-core machine, you will likely see processor use briefly exceed 90 percent each time the graph is generated.