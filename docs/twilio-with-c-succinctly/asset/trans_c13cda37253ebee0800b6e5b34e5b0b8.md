

```xml
<Conference startConferenceOnEnter="false" endConferenceOnExit="false" muted="false" waitUrl="http://bit.ly/20gwxz4">CoolestConf</Conference>
</Dial>
</Response>
```

请注意，当使用扬声器时，**startConferenceOnEnter** 和 **endConferenceOnExit** 的值均设置为 **false**，并且 **muted** 也设置为 **false**。

最后，让我们看看为作为主持人加入的人生成的 XML 响应。

*代码清单 36：主持人的 TwiML 标记响应*

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

请注意，当使用主持人时，**startConferenceOnEnter** 和 **endConferenceOnExit** 的值均设置为 **true**，并且 **muted** 也设置为 **false**。

为了测试这一点，只需使用 Visual Studio 中的发布选项将其部署到 Azure Websites。拨打你的 Twilio 号码，准备就绪。

为了测试此功能，模拟两个用户加入会议，你至少需要两部电话。Twilio 通过几行代码和几个动词及属性所能实现的功能非常酷。

显然，可以为这个会议演示添加更多功能，例如宣布呼叫者的姓名、录制会议以及其他交互式语音选项。可能性是无限的。

我建议你访问 Twilio 文档，以了解 **Conference** 动词提供的其他所有属性并探索其他可能性。

让我们继续，看看我们的最后一个示例。我们将看看如何实现自动语音调查解决方案，这应该很有趣且令人兴奋。

## 自动语音调查

自动调查允许最终用户拨打一个电话号码，该电话号码将用于执行询问问题并提示用户提供每个问题答案的调查。

电话调查是从用户那里收集有价值数据的好方法，并且它们有许多业务应用，特别是在品牌知名度、产品洞察和客户满意度方面。

首先，让我们解释一下使用 Twilio 时语音调查应该如何工作。

- Twilio 接收呼叫并向我们的 TwilioSuccinctly TwiML 应用发起 HTTP 请求——例如，请求关于如何响应的说明。
- NancyFX 应用指示 Twilio（使用 TwiML）收集用户的语音输入。用户将被要求提供一个唯一的 ID，我们将通过该 ID 识别他们。
- 在每个问题之后，Twilio 将携带用户输入再次向我们的 NancyFX 应用发起请求，我们的应用程序会将这些数据存储在 Azure 表中。
- 存储答案后，应用程序将继续指示 Twilio 将用户重定向到下一个问题，直到调查结束。简而言之，这就是语音调查应用应该做的事情。

我们将扩展我们的 SimpleAnsweringMachine 类，包含一个将数据保存到我们称为 ResponsesSuccinctly 的 Azure 表中的方法。

我们的 ResponsesSuccinctly 表有三个字段。在 PartitionKey 中，我们将存储问题 ID。在 RowKey 中，我们将存储用户 ID。最后，我们将有一个名为 Response 的第三个字段，它也将是一个字符串，并将包含用户的响应。

我们还需要另外两个表——一个名为 Questions，将包含问题 ID（PartitionKey）以及作为字符串的实际问题本身。我们还需要一个 PredefinedAnswers 表，将包含每个问题的可能答案。

因此，我们的调查应用将从 Questions 和 PredefinedAnswers 表中读取，并将用户输入存储在 Azure 上的 ResponsesSuccinctly 表中。

让我们使用 Azure Storage Explorer 创建 Questions 和 PredefinedAnswers 表。我们将从 Questions 表开始，并用示例数据填充它。

![](img/7d3e41c7ef83c5fb4ef242998ad60317_89_0.png)

图 52：Azure 上的 Questions 表

你可以看到，表的 **RowKey** 是问题本身的简短 ID 表示形式，而实际问题存储在也是字符串的 **Question** 字段中。

现在让我们使用 Azure Storage Explorer 创建 PredefinedAnswers 表，并用此示例数据填充它。

![](img/7d3e41c7ef83c5fb4ef242998ad60317_89_1.png)

图 53：Azure 上的 PredefinedAnswers 表

在 PredefinedAnswers 的 **PartitionKey** 中，我们存储答案编号，在 **RowKey** 中，我们存储问题编号。作为字符串的 **Answer** 字段包含实际答案本身。

我们可以看到所有问题都有多个预定义答案，有些比其他的多，这些将是提供给用户的选项。然后，他们的答案将存储在 ResponsesSuccinctly 表中。

既然理论部分已经掌握，让我们写一些代码。首先，让我们将我们的 TwiML 应用指向我们的新端点，我们将把它称为 /survey/incoming。

## 语音

![](img/7d3e41c7ef83c5fb4ef242998ad60317_90_0.png)

*图 54：用于我们 TwilioSuccinctly TwiML 应用的语音请求 URL*

现在，让我们定义我们的调查问候语。我们将修改我们的 **AnsweringMachineMain** NancyFX 模块以适应这种情况。

*代码清单 37：自动语音调查问候语*

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

问候语要求呼叫者提供社会安全号码以进行身份验证。请记住，在非演示场景中，你永远不会向用户索要社会安全号码！当信息收集完成后，将向 /survey/connect REST 端点发送请求，该端点将处理剩余的调查逻辑。我们稍后需要稍作修改此代码以初始化状态（我们稍后将会讨论这一点）。

社会安全号码值将存储在 ResponsesSuccinctly 表中，并将识别用户提供相应答案的用户。

应用程序不会对社会安全号码进行任何验证（为了验证它是有效或唯一的数字），因为目的只是为了演示如何通过交互式选项收集信息。该应用程序始终可以通过更具体的逻辑进行改进和扩展，以验证此或其他方面。

在我们深入 /survey/connect 端点的细节之前，我们需要为我们的 **SimpleAnsweringMachine** 类添加额外功能，包含一个将数据保存到 ResponsesSuccinctly 表的方法，并且我们需要添加几个从 Questions 和 PredefinedAnswers 表中获取信息的方法。

让我们现在创建一个从 Questions 表中读取的方法，以及另一个从 PredefinedAnswers 表中读取的方法。

我们需要创建一个 **QuestionsData** 类，对应于 Questions Azure 表的结构。代码清单 38 展示了我们如何定义此类。

*代码清单 38：QuestionsData 类*

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

我们还需要在我们的 `SimpleAnsweringMachine` 类中包含代码清单 39 的 **using** 语句，因为我们将使用 `List<string>` 来从 Questions 表中获取问题。

*代码清单 39：使用 System.Collections.Generic*

```csharp
using System.Collections.Generic;
```

并且，我们需要在我们的 `SimpleAnsweringMachine` 类中包含代码清单 40 的常量。

*代码清单 40：我们 SimpleAnsweringMachine 类的其他常量*

```csharp
private const string cStrSurveyResponses = "ResponsesSuccinctly";
private const string cStrSurveyQuestions = "Questions";
private const string cStrSurveyAnswers = "PredefinedAnswers";
```

现在，让我们在我们的 `SimpleAnsweringMachine` 类中实现 `GetQuestions` 方法。

*代码清单 41：GetQuestions 方法*

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

