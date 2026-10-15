different datasets. Back in the main method of our program, let's leverage our JSON data and the new SurveyResults class to improve our setup. Currently, we collect input from the user to select a report to run, but we do not ask them what time frame they would like to pull that data from.

```
do
{
    Console.WriteLine("Please specify a report to run (rewards, comments, tasks, quit):");
    var selectedReport = Console.ReadLine();

    Console.WriteLine("Please specify which quarter of data: (q1, q2)");
    var selectedData = Console.ReadLine();

    var surveyResults = JsonConvert.DeserializeObject<SurveyResults>
        (File.ReadAllText($"data/{selectedData}.json"));

    switch (selectedReport)
    {
```

So below our first input, let's add another Console.WriteLine statement that says please specify which quarter of data, and again, provide some examples in parentheses like (q1, q2) or so on. Below that, let's add another variable called selectedData and set that to equal another Console.Read line for whatever they enter. Next, we need to read in our JSON file and map it to our SurveyResults class. For this, I'm just going to paste in a line of code that you can use for reference since it does require a few concepts that are beyond the scope of our discussion. This code uses the .NET file helper class that we looked at earlier to read in our raw JSON data files. We also pass in the selectedData variable as part of that file path to grab the data file the user selected. We then use the JsonConvert class, which is also provided by .NET to map the broad data to an instance or usable object of our SurveyResults class. That object is stored in a surveyResults variable, which we can use to access our survey data just like we did previously with our Q1Results class. Now, because the survey results are now stored in a variable that is