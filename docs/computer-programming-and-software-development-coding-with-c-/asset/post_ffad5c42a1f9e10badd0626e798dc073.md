
# Chapter 14 Program Flow Considerations with Dynamic Data

Let's explore how to update our app and program flow to work with more dynamic sets of data. Throughout this book, we have utilized a static or dataset that we've called Q1Results. This represents a set of exported data that Wired Brain would receive from their simple survey tool for the first quarter of the year. However, as the year goes on, they would like to be able to analyze the results from the second, or third and fourth quarters as well. Right now, our app cannot easily adapt to that scenario, so let's see how to improve this situation. In a real app designed to process survey results, we, of course, would not just receive a C# class with values in it. Using globally available static values like this is actually a bad practice in many situations. Instead, we would retrieve that data from a web service or database, or perhaps through exported files in simpler cases.

```
public static class Q1Results
{
    // Aggregate ratings
    public static double ServiceScore { get; set; } = 8.0;
    public static double CoffeeScore { get; set; } = 4.0;
    public static double PriceScore { get; set; } = 6.0;
    public static double FoodScore { get; set; } = 7.5;
    public static double WouldRecommend { get; set; } = 6.5;
    public static string FavoriteProduct { get; set; } = "Cappuccino";
    public static string LeastFavoriteProduct { get; set; } = "Granola";
    public static string AreaToImprove { get; set; } = "MobileApp";

    // Aggregate counts
    public static double NumberSurveyed { get; set; } = 500;
}
```

That data would also be scoped more carefully to the required methods that use it and managed by our program flow. Let's pursue that option of using file exports to get our data. Each of these files represents the exported survey results for a different quarter of the year, and of course, more would be added as time goes on, so Q3 and Q4, and then future years. If you're not familiar with JSON or JavaScript Object Notation, as it's formally called, it's a very common type of data format. Despite the name reference to JavaScript, it's a fairly way to define and transfer data between different apps. So let's open up our Q1Results.json, and right away, we can see that structurally, it is very close to our original Q1Results C# file. JSON uses objects, arrays, and key value pairs to hold sets of data.

```
{
  "serviceScore": 8.0,
  "coffeeScore": 5.0,
  "priceScore": 6.0,
  "foodScore": 7.5,
  "wouldRecommend": 6.5,
  "favoriteProduct": "Cappuccino",
  "leastFavoriteProduct": "Granola",
  "areaToImprove": "MobileApp",
  "numberSurveyed": 500.0,
  "numberResponded": 325.0,
  "numberRewardsMembers": 130.0,
  "responses": [
    {
      "serviceScore": 8.5,
      "coffeeScore": 8.0,
      "priceScore": 7.0,
      "foodScore": 9.0,
      "wouldRecommend": 8.0,
      "favoriteProduct": "Latte",
      "leastFavoriteProduct": "Fruit",
      "areaToImprove": "MobileApp",
      "isRewardsMember": false,
      "emailAddress": "test1@sample.com",
      "comments": "Your mobile app is too slow."
    },
    {
```

In fact, I can open these up side by side just to compare. So, I'll rearrange these real quick, and of course, we can see that they are very similar.

```
"coffeeScore": 5.0,
"priceScore": 6.0,
"foodScore": 7.5,
"wouldRecommend": 6.5,
"favoriteProduct": "Cappuccino",
"leastFavoriteProduct": "Granola",
"areaToImprove": "MobileApp",
"numberSurveyed": 500.0,
"numberResponded": 325.0,
"numberRewardsMembers": 130.0,
"responses": [
{
"serviceScore": 8.5,
"coffeeScore": 8.0,
"priceScore": 7.0,
"foodScore": 9.0,
"wouldRecommend": 8.0,
"favoriteProduct": "Latte",
"leastFavoriteProduct": "Fruit",
"areaToImprove": "MobileApp",
"isRewardsMember": false,
"emailAddress": "test1@sample.com",
"comments": "Your mobile app is t
}
{
public static class Q1Results
{
// Aggregate ratings
public static double ServiceScore { get; set; } = 8.0;
public static double CoffeeScore { get; set; } = 4.0;
public static double PriceScore { get; set; } = 6.0;
public static double FoodScore { get; set; } = 7.5;
public static double WouldRecommend { get; set; } = 6.5;
public static string FavoriteProduct { get; set; } = "Cappuccino"
public static string LeastFavoriteProduct { get; set; } = "Granola"
public static string AreaToImprove { get; set; } = "MobileApp"
// Aggregate counts
public static double NumberSurveyed { get; set; } = 500;
```

We have our aggregate scores at the top, such as our coffee score or service score and so on, as well as our individual responses with our comments down below. In JSON, those comments are represented by an array, just like we used a list in our C# code, and if we were to open up the second quarter JSON file, we can, of course, see the same structure, but with a more recent or updated set of values. Well, we want our updated app to be able to read in these JSON files dynamically. Because our JSON keys have the same names and structure as the C# properties of this class, we could map them over to our class to use throughout the app. We could also enable the user to select which file to pull data from to run our reports, just like we previously allowed them to select which report to run. So to start with, let's prep this Q1Results class to be more reusable and be able to handle mappings from our JSON file. First, let's just step through here and delete all of the value assignments. We no longer need these values, since they will be pulled from our new datasets and mapped to these properties. So just take a moment to go through these, and at the bottom, also make sure to delete the list of individual responses. You can replace that list with get and set accessors like the other properties up here, so we'll be able to map the array of responses from the JSON. Let's also get rid of the static keyword everywhere in this file. In simplified terms, static makes these properties globally available across our app by associating them with the Q1Results class directly, rather than an object instance of that class. If you are not entirely sure what that means yet, no worries, just make sure that you remove them for now. The last thing we need to do is rename this class. So I'll just switch this to something more reusable or generic like SurveyResults. Make sure to also rename the survey results file in the Solution Explorer, which is an easy step to forget.

```
public class SurveyResults
{
    // Aggregate ratings
    public double ServiceScore { get; set; }
    public double CoffeeScore { get; set; }
    public double PriceScore { get; set; }
    public double FoodScore { get; set; }
    public double WouldRecommend { get; set; }
    public string FavoriteProduct { get; set; }
    public string LeastFavoriteProduct { get; set; }
```

When you're finished, if we were to try and build the app, we'll get a lot of errors in our consult, since we've broken the references to our Q1Results class. Next, let's see how to complete this setup by dynamically selecting and loading in our JSON data. Let's finish enhancing our app's program flow to be able to dynamically process different datasets. Back in the main method of our program, let's leverage our JSON data and the new SurveyResults class to improve our setup. Currently, we collect input from the user to select a report to run, but we do not ask them what time frame they would like to pull that data from.

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
