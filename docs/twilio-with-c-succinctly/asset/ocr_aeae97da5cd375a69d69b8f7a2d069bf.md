```
```csharp
public string InsertSpace(string s)
{
    string res = string.Empty;

    int count = 1;
    foreach (char c in s)
    {
        if (char.IsDigit(c) && count < s.Length)
            res += c + " ";
        else
            res += c;

        count++;
    }
    return res;
}
```
```

If you now publish this application within Visual Studio to Azure Websites, when you dial your Twilio number you should now hear the phone menu, be able to enter 1, 2, or 3, and get connected to the phone number that corresponds to the option selected. This is possible thanks to the data stored on the Azure table.

This example could be further improved with more interactivity, but that's beyond the scope of what we'll cover here. However, you are encouraged to check out the Twilio documentation and keep adding more features.

Let's build some other cool examples.

# Simple conferencing service

Services such as PowwowNow, WebEx, or GotoMeeting that allow you to dial a conference call number, set up a virtual meeting room, and speak to other people are known as conferencing services.

Twilio also allows us to build these kind of services. We'll explore the basics of how we can set up a small conferencing app.

First, let's expand our NancyFX app in order to include this functionality.

In the same way we configured our phone menu, let's configure our Twilio number to point to a specific URL that our web app will use for processing incoming calls.

Next let's modify our TwiML app called TwilioSuccinctly to point to our new incoming URL. This URL should contain the location of our NancyFX app on Azure Websites followed by /conf/incoming.