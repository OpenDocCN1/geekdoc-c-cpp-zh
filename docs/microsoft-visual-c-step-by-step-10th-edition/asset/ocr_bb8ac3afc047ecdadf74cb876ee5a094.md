![](bbox=[0.172, 0.093, 0.866, 0.258])

# Note

If you have a quad-core computer, you can increase the CPU use and further reduce the time by adding two more Task objects and dividing the work into four chunks in the plotButton_Click method, as shown here in bold:

Click here to view code image

```
Task first = Task.Run(() => generateGraphData(data, 0, pixelWidth / 8));nTask second = Task.Run(() => generateGraphData(data, pixelWidth / 8, pixelWidth / 4));nTask third = Task.Run(() => generateGraphData(data, pixelWidth / 4, pixelWidth * 3 / 8));nTask fourth = Task.Run(() => generateGraphData(data, pixelWidth * 3 / 8, pixelWidth / 2));nTask.WaitAll(first, second, third, fourth);
...
```

If you have only a dual-core processor, you can still try this modification, and you should notice a small beneficial effect on the time. This is primarily because of how the algorithms used by the CLR optimize the way in which the threads for each task are scheduled.

# Abstracting tasks by using the Parallel class