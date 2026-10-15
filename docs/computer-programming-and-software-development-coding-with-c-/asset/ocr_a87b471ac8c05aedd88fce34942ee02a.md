delete the list of individual responses. You can replace that list with get and set accessors like the other properties up here, so we'll be able to map the array of responses from the JSON. Let's also get rid of the static keyword everywhere in this file. In simplified terms, static makes these properties globally available across our app by associating them with the Q1Results class directly, rather than an object instance of that class. If you are not entirely sure what that means yet, no worries, just make sure that you remove them for now. The last thing we need to do is rename this class. So I'll just switch this to something more reusable or generic like SurveyResults. Make sure to also rename the survey results file in the Solution Explorer, which is an easy step to forget.

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

When you're finished, if we were to try and build the app, we'll get a lot of errors in our consult, since we've broken the references to our Q1Results class. Next, let's see how to complete this setup by dynamically selecting and loading in our JSON data. Let's finish enhancing our app's program flow to be able to dynamically process