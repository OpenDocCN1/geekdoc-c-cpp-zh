
## Make outbound calls

We've seen how we can receive calls and process voice requests using TwiML. Before closing this chapter and moving into more advanced examples, let's discuss how we can make outbound calls using the Twilio C# helper library.

We'll expand our **TwilioCore** class and add a method to make calls. Let's implement this method in Code Listing 26.

### Code Listing 26: The TwilioCore StartCall Method

```csharp
public void StartCall(string from, string to, string url)
{
    // SID = Twilio AccountSID, aTk = Twilio AuthToken
    if (SID != string.Empty && aTk != string.Empty && from !=
        string.Empty && to != string.Empty)
    {
        TwilioRestClient client = new TwilioRestClient(SID, aTk);
        client.InitiateOutboundCall(from, to, url);
    }
}
```

As you can see, the **StartCall** method is very simple. It has two parameters: **from** and **to**, which, respectively, represent the caller and receiver phone numbers.

The third parameter is a URL resource that the person on the other side of the phone will hear once the call is picked up. This URL needs to return a valid TwiML response.

As we've been doing all along when using our **TwilioCore** class methods, let's implement a wrapper method around **StartCall** that we can invoke from the **Main program**.

### Code Listing 27: The StartRecordedCall Wrapper Method

```csharp
public static void StartRecordedCall()
{
    using (TwilioCore tc = new TwilioCore(cStrSid, cStrAuthTk))
    {
        tc.StartCall(cStrSender, cStrReceiver,
            "http://www.edfreitas.me/twilio/sayhello.xml");
    }
}
```

Now, we can call this method from the **Main program**.

### Code Listing 28: Calling the StartRecordedCall Wrapper Method from the Main Program

```csharp
static void Main(string[] args)
{
    TwilioExample.StartRecordedCall();

    Console.ReadLine();
}
```

When executing this code, you should hear a recording on the phone number that you have indicated as **cStrReceiver** within your **TwilioExample** class.

As we've seen, making outbound calls with Twilio is easy. In just a few lines of code, we've been able to start a phone call and play a message.

If the destination number you will be dialing is an international (non-US) number, you'll need to enable certain permissions to allow Twilio to perform that action. These permissions can be checked and configured at this URL.

You can also adapt this code to enable the application to give a personalized message or record reactions to it.

## Summary

In this chapter, we've started to scratch the surface of what is possible with Twilio's voice-enabled features.

We've seen how to receive incoming calls, give specific feedback based on a user's input, and make outbound calls.

We've also seen how to set up a quick NancyFX Azure website in order to create a simple answering machine.

In the next chapter, we'll dig a bit deeper into using Twilio's voice-enabled features and create some interesting and more advanced samples that can be useful in a business context.

# Chapter 4 Automation Using Voice

## Introduction

We've explored the basics of Twilio's voice capabilities, which has hopefully given you a good idea of what is possible to do with TwiML and the C# helper library in order to create voice-enabled applications.

Let's now explore how we can expand a bit more and use Twilio's voice-enabled features in order to automate business processes.

We'll mostly use TwiML in order to create an interactive phone menu, a simple conferencing service, and an exciting, automated voice-survey solution.

We'll also be relying on Azure Table Storage and Azure Websites, just as in Chapter 3, and because we are basing the code that follows on Chapter 3's code, the examples should again be easy to follow and fun to implement.

## Interactive Phone Menu

An Interactive Phone Menu is an automated phone software system that can facilitate and coordinate the communication between callers and businesses. If you've ever dialed your insurance company to file a claim and responded to a series of automated prompts, you've used one of these systems.

Twilio makes it easy to build this. We've already explored some of the basics by building a simple answering machine in Chapter 3. Now, let's create a phone menu system for a company that has departments located in different regions. This system will connect the caller with a specific department based on the digit entered by the caller.

In order to start the phone menu, we need to configure our Twilio number so that it will send our web application an HTTP request when we receive an incoming call. We'll use and modify the existing NancyFX app we created in the previous chapter.

First, we configure our Twilio number to point to a specific URL that our web app will use for processing incoming calls. Next, we modify the TwiML app we called **TwilioSuccinctly** to point to our new incoming URL. This URL should be the location of our NancyFX app on Azure Websites followed by `/ipm/incoming`.

### TwilioSuccinctly

| Property | Value |
| :--- | :--- |
| **SID** | *content obscured* |
| **Friendly Name** | TwilioSuccinctly |
| **Voice** | |
| Request URL | http://twiliosuccinctly.azurewebsites.net/ipm/incoming | HTTP GET |
| **Messaging** | |
| Request URL | *(empty input field)* | HTTP POST |

**Save** **Cancel**

![](img/7d3e41c7ef83c5fb4ef242998ad60317_79_0.png)

Based on Figure 48, we'll assume our phone menu app will receive incoming calls through this REST endpoint: `/ipm/incoming`.

We'll use this to greet our callers. Let's add this endpoint logic on our **AnsweringMachineMain** NancyFX module.

### Code Listing 29: The Interactive Phone Menu Greeting

```csharp
// In NancyFX, _ = > indicates that no parameters are used for this route.
Get["/ipm/incoming"] = _ =>
{
    string res = "<Response>" +
        "<Gather action=\"/ipm/response\" method=\"GET\">" +
        "<Say voice=\"woman\">Welcome to Cool Company.</Say>" +
        "<Say voice=\"woman\">Press 1 to contact Sales.</Say>" +
        "<Say voice=\"woman\">Press 2 to contact Support.</Say>" +
        "<Say voice=\"woman\">Press 3 for general inquiries.</Say>" +
        "</Gather>" +
        "<Say voice=\"woman\">We didn't get any response. Bye.</Say>" +
        "</Response>";

    return Response.AsText(res, "text/xml");
};
```

Using Visual Studio, let's publish our NancyFX application with this change to Azure Websites. If we then call our Twilio number, we should now hear this response. Hurray!

Moving forward, the **Gather** verb on the TwiML response points to another endpoint: `/ipm/response`. We'll use this endpoint to create our menu response based on the input entered by the caller.

Note that we can still use and expand our **SimpleAnsweringMachine** class in order to add any specific logic required for our phone menu.

Having a method that inserts a space after each char within a string is also useful. This is done so that Twilio can read the phone number digit-by-digit rather than by reading the entire number at once. We'll explore that in a bit.

First, let's process the caller's input and create our `/ipm/response` endpoint on our **AnsweringMachineMain** NancyFX module.

Just as we did with our simple answering machine example in Chapter 3, we'll query the **SASuccinctly** table on Azure and retrieve a value.

However, this value will be a phone number that corresponds to the option the user entered. The digit the user entered will be the **PartitionKey** and the phone number retrieved will be the **RowKey**. The phone number needs to be in an international format, i.e. +14800001111.

Let's add three more rows to our **SASuccinctly** table using Azure Storage Explorer.

![](img/7d3e41c7ef83c5fb4ef242998ad60317_80_0.png)

This phone number will be used to connect the caller with the corresponding department within the company.

### Code Listing 30: The Interactive Phone Menu Response Endpoint

```csharp
Get["/ipm/response"] = _ =>
{
    string num = "Unknown";
    // ... code continues
}
```
