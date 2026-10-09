
```xml
<Conference startConferenceOnEnter="false" endConferenceOnExit="false" muted="false" waitUrl="http://bit.ly/20gwxz4">CoolestConf</Conference>
</Dial>
</Response>
```

Notice that with a speaker, the **startConferenceOnEnter** and **endConferenceOnExit** values are set to **false** and **muted** is set to **false**.

Finally, let’s examine the XML response generated for a person who joins as a moderator.

*Code Listing 36: The TwiML Markup Response for a Moderator*

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Response>
  <Say voice="woman">You entered: 7</Say>
  <Say voice="woman">You're being connected to the conference now as, please hold on.</Say>
  <Pause length="2"/>
  <Say voice="woman">You have joined the conference.</Say>
  <Dial>
    <Conference startConferenceOnEnter="true" endConferenceOnExit="true"
     muted="false" waitUrl="http://bit.ly/20gwxz4">CoolestConf</Conference>
  </Dial>
</Response>
```

Notice that with a moderator, the **startConferenceOnEnter** and **endConferenceOnExit** values are set to **true** and **muted** is set to **false**.

In order to test this, simply deploy to Azure Websites by using the publish option within Visual Studio. Call your Twilio number and you are ready to go.

You’ll need at least two phones in order to test this by simulating two users joining the conference. It’s pretty cool what Twilio can do with a few lines of code and a couple of verbs and attributes.

Obviously, more functionality could be added to this conferencing demo, such as announcing the names of the callers, recording the conference, and other interactive voice options. The possibilities are endless.

I encourage you to visit the Twilio documentation to learn more about all the attributes that the **Conference** verb offers and to explore other possibilities.

Let’s move on and look at our final example. We’ll see how we can implement an automated voice survey solution, which should be quite interesting and a lot of fun.

## Automated voice survey

An automated survey allows end users to call a phone number that will be used to conduct a survey that asks questions and prompts the user to provide answers to each question.

Phone surveys are a great way to gather valuable data from our users, and they have many business applications, especially in regards to brand awareness, product insights, and customer satisfaction.

First, let's explain how a voice survey should work using Twilio.

- Twilio gets the call and makes an HTTP request to our TwilioSuccinctly TwiML application— e.g., asking for instructions on how to respond.
- The NancyFX app instructs Twilio (using TwiML) to Gather the user's voice input. The user will be asked to provide a unique ID, and we'll identify them by that.
- After each question, Twilio will make another request to our NancyFX app with the user's input, which our application stores on an Azure table.
- After storing the answer, the app will continue instructing Twilio to redirect the user to the next question until the survey is finished. In a nutshell, that's what the voice survey app should do.

We'll expand our SimpleAnsweringMachine class to include a method that saves data on an Azure table we'll call ResponsesSuccinctly.

Our ResponsesSuccinctly table has three fields. On the PartitionKey, we'll store the question's ID. On the RowKey, we'll store the user's ID. Finally, we'll have a third field called Response that will also be a string and will contain the user's response.

We'll also need two other tables—one called Questions that will contain the ID of the question (PartitionKey) and the actual question itself as a string. We'll also need a PredefinedAnswers table that will contain possible answers for each question.

So, our survey app will read from the Questions and PredefinedAnswers tables and store the user's input on the ResponsesSuccinctly table on Azure.

Let's create the Questions and PredefinedAnswers tables using Azure Storage Explorer. We'll start with the Questions table and populate it with sample data.

![](img/7d3e41c7ef83c5fb4ef242998ad60317_89_0.png)

Figure 52: The Questions Table on Azure

You can see that the **RowKey** of the table is a short ID representation of the question itself, and the actual question is stored on the **Question** field, which is also a string.

Let’s now create the PredefinedAnswers table with Azure Storage Explorer and populate it with this sample data.

![](img/7d3e41c7ef83c5fb4ef242998ad60317_89_1.png)

Figure 53: The PredefinedAnswers Table on Azure

On the PredefinedAnswers **PartitionKey**, we store the answer number and on the **RowKey** we store the question number. The **Answer** field, which is a string, contains the actual answer itself.

We can see all questions have multiple predefined answers, some more than others, and these will be the options presented to the users. Their answers will then be stored on the ResponsesSuccinctly table.

With the theory behind us, let’s write some code. First, let’s point our TwiML app to our new endpoint, which we will call /survey/incoming.

## Voice

![](img/7d3e41c7ef83c5fb4ef242998ad60317_90_0.png)

*Figure 54: Voice Request URL for Our TwilioSuccinctly TwiML App*

Now, let's define our survey greeting. We'll modify our **AnsweringMachineMain** NancyFX module to accommodate for this.

*Code Listing 37: The Automatic Voice Survey Greeting*

```csharp
Get["/survey/incoming"] = _ =>
{
    string res = "<Response>" +
        "<Gather action=\"/survey/connect\" method=\"GET\">" +
        "<Say voice=\"woman\">You are about to join the UFO survey.</Say>" +
        "<Say voice=\"woman\">What is your Social Security Number?</Say>" +
        "</Gather>" +
        "<Say voice=\"woman\">We didn't get any response. Bye.</Say>" +
        "</Response>";

    return Response.AsText(res, "text/xml");
};
```

The greeting requests that the caller provide a Social Security Number for identification. Keep in mind that in a non-demo scenario, you'd never ask a user for a Social Security Number! When the information has been gathered, a request will be sent to the /survey/connect REST endpoint, which will handle most of the remaining survey logic. We'll later need to slightly modify this code in order to initialize state (we will cover this later).

The Social Security Number value will be stored on the ResponsesSuccinctly table and will identify the user with the corresponding answers provided.

The application will not do any validation on the Social Security Number (in order to verify if it is a valid or unique number), as the purpose is to simply demonstrate how the information can be gathered through interactive options. The application can always be improved upon and expanded with more specific logic that can validate this or other aspects.

Before we dig into the details of the /survey/connect endpoint, we need to add extra features to our **SimpleAnsweringMachine** class to include a method that saves data to the ResponsesSuccinctly table, and we need to add a couple of other methods that fetch information from the Questions and PredefinedAnswers tables.

Let's now create a method that reads from the Questions table and another that reads from the PredefinedAnswers table.

We'll need to create a **QuestionsData** class that corresponds to the structure of the Questions Azure table. Code Listing 38 shows how we can define this class.

*Code Listing 38: The QuestionsData Class*

```csharp
public class QuestionsData : TableEntity
{
    public QuestionsData(string p, string d)
    {
        PartitionKey = p;
        RowKey = d;
    }
    public QuestionsData()
    {
    }
    public string Question { get; set; }
}
```

We'll also need to include Code Listing 39's **using** statement on our `SimpleAnsweringMachine` class, as we'll be using `List<string>` in order to get the questions from the Questions table.

*Code Listing 39: Using System.Collections.Generic*

```csharp
using System.Collections.Generic;
```

And, we'll need to include Code Listing 40's constants to our `SimpleAnsweringMachine` class.

*Code Listing 40: Additional Constants for Our SimpleAnsweringMachine Class*

```csharp
private const string cStrSurveyResponses = "ResponsesSuccinctly";
private const string cStrSurveyQuestions = "Questions";
private const string cStrSurveyAnswers = "PredefinedAnswers";
```

Now, let's implement the `GetQuestions` method within our `SimpleAnsweringMachine` class.

*Code Listing 41: The GetQuestions Method*

```csharp
public string[] GetQuestions()
{
    List<string> q = new List<string>();
    try
    {
        var storageAccount = CloudStorageAccount.Parse(cStrConnStr);
        CloudTableClient tableClient =
            storageAccount.CreateCloudTableClient();
        CloudTable table =
```
