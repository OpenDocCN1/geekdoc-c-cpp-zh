| ACTIVITY | DESCRIPTION |
|---|---|
| Delay | Pauses the flow of the workflow. This is typically used to schedule some event. For example, you might have a workflow that is responsible for printing a daily report. The Delay activity could be used to schedule this printout so that it is ready as the workers come in to read it. You can either set the delay explicitly by setting the TimeoutDuration property or set it via code using the event identified in the InitializeTimeoutDuration property. |
| Suspend | Temporarily stops the workflow. This is usually due to some extraordinary event that you would want an administrator or developer to correct. The workflow will continue to receive requests, but not complete them past the Suspend activity. The administrator may then resume the workflow to complete processing. |
| Terminate | Ends the workflow immediately. This should only be done in extreme situations such as when the workflow is not capable of any further processing (e.g., it has lost the connection to a database or other needed resource). |
| Throw | Creates an exception that can be caught by the code hosting the workflow. This provides a means of propagating an error from the workflow to the containing code. |

# Building Custom Activities

In addition to the standard activity library, WF supports extensibility through the creation of custom activities. Creating custom activities is a matter of creating a new class that inherits from Activity (or one of the existing child classes). Several available attributes enable customization of the activity and how it appears when you use it in your workflows.

Creating custom activities is the primary means of extending WF. You might use custom activities to simplify a complex workflow, grouping a number of common activities into a single new activity. Alternatively, custom activities can create a workflow that is easier to understand, using terms that are more familiar to the developers and business experts. Finally, custom activities can be used to support software used within the business, such as activities to communicate with a existing system.

So you can see the steps required for creating a custom activity, the next exercise creates a simple activity that wraps the Google translation service. Create a new project using the Workflow Activity Library template, called TranslationActivity. Again, you will have to target the .NET Framework 3.5 to view the correct template. This project will create a DLL that contains the activities you create. It will include a single custom activity initially. This activity inherits from SequenceActivity, so it might include multiple child activities. You can change this as needed, but it’s a good enough default for most activities. Drag a Code activity onto the designer. This activity does the actual translation work.

Because the new activity will be used to convert between a number of set language pairs, create an enumeration containing the valid options. This enumeration can be expanded as new options become available:

```
Public Enum TranslationOptions As Integer
    EnglishToFrench
    EnglishToSpanish
    EnglishToGerman
    EnglishToItalian
    EnglishToRussian
    EnglishToChinese
    FrenchToEnglish
    SpanishToEnglish
    GermanToEnglish
    ItalianToEnglish
    RussianToEnglish
    ChineseToEnglish
End Enum
```