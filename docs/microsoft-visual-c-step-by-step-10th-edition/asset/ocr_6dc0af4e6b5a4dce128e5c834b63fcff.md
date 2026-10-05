![](bbox=[0.165, 0.085, 0.835, 0.465])

4. When the Graph Demo application starts, select Plot Graph.
5. Wait for a few seconds, and then select Plot Graph again.
6. Repeat step 4 several times, waiting a few seconds between selections.
7. Close the application and return to Visual Studio.
   Performance Profiler generates a report showing how the CPU was used. The graph at the top of the report should show several flat-topped peaks. These peaks will correspond to each time you selected Plot Graph.
8. Hover over one of the peaks to view the CPU use at that point. In the following image, the maximum CPU use is around 25%. In my case, the application was running on a quad-core machine, but it looks as though the app is only using a single processor: