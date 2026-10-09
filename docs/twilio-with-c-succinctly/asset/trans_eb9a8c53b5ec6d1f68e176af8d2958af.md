

TableQuery.GenerateFilterCondition("RowKey",
QueryComparisons.Equal, "q" + qn));

foreach (PredefinedAnswersData en in
table.ExecuteQuery(query))
{
    pa.Add(en.PartitionKey + "|" + en.Answer);
}
catch (Exception ex)
{
    Console.WriteLine(ex.ToString());
}

return pa.ToArray();
}

public void InsertSurveyResponse(string qId, string uId,
    string aId)
{
    try
    {
        var storageAccount =
            CloudStorageAccount.Parse(cStrConnStr);
        CloudTableClient tableClient =
            storageAccount.CreateCloudTableClient();
        CloudTable table =
            tableClient.GetTableReference(cStrSurveyResponses);

        TableOperation retrieveOperation =
            TableOperation.Retrieve<ResponseData>(qId, uId);

        TableResult retrievedResult =
            table.Execute(retrieveOperation);
        ResponseData updateEntity =
            (ResponseData)retrievedResult.Result;

        if (updateEntity == null)
        {
            updateEntity = new ResponseData();
            updateEntity.PartitionKey = qId;
            updateEntity.RowKey = uId;
            updateEntity.Response = aId;
        }

        TableOperation insertOrReplaceOperation =
            TableOperation.InsertOrReplace(updateEntity);
table.Execute(insertOrReplaceOperation);
}
catch (Exception ex)
{
    Console.WriteLine(ex.ToString());
}
}

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
} // 类 SimpleAnsweringMachine 结束
} // 命名空间 TwilioSuccinctly 结束

有了我们最新的 SimpleAnsweringMachine 逻辑，让我们将注意力转移到 AnsweringMachineMain NancyFX 模块，以便我们可以编写 /survey/connect REST 端点的逻辑。

调查应用程序应获取所有问题列表，遍历每个问题，向调用者展示可用的预定义答案，然后存储每个响应。

为了在 AnsweringMachineMain NancyFX 模块上保持状态并了解将向调用者询问哪些问题，我们需要创建一些受保护的 AnsweringMachineMain 类级属性。

我们需要维护状态，因为 /survey/connect 端点对每个新的问题和答案都会调用自身，因此我们需要知道哪些内容已被回答。

*代码清单 46：用于维护 AnsweringMachineMain 状态的受保护类级属性*

```
// 状态成员变量使用 protected 修饰符声明，以便在类被继承时使用。
protected static string[] questions = null;
protected static int currentQuestion = 0;
protected static string userId = string.Empty;
```

**questions 字符串**数组保存调用者将被要求回答的问题名称。

**currentQuestion 整型**变量保存当前正在提示用户回答的问题的状态。

最后，**userId 字符串**表示用于识别调用者为每个问题提供的答案的社会安全号码（唯一标识符）的值。

为了简单起见，并为了避免唯一标识符被误认为是对问题的回答，我们演示中对社会安全号码的唯一要求是用户输入至少包含两个字符的任何值。

正如大家记得的那样，我们之前已经解决了需要适应 /survey/incoming 端点以初始化状态的问题。我们将在代码清单 47 中对其进行修改。

# *代码清单 47：带有状态初始化的 /survey/incoming REST 端点*

```
Get[@"/survey/incoming"] = _ =>
{
    userId = string.Empty;
    currentQuestion = 0;
    questions = null;

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

有了状态初始化，我们可以创建 /survey/connect 端点逻辑，所有的“魔法”将在那里发生。

# *代码清单 48：/survey/connect REST 端点*

```
Get[@"/survey/connect"] = _ =>
{
    string res = "<Response><Say voice=\"woman\">No valid option entered.</Say></Response>";
    string val = Request.Query["Digits"].Value;
    if (val != null && val != string.Empty)
    {
        using (SimpleAnsweringMachine sam = new SimpleAnsweringMachine())
        {
            if (userId == string.Empty)
            {
                if (val.Length > 1)
                {
                    userId = val;

                    if (questions == null)
                        questions = sam.GetQuestions();

                    res = ProcessQuestion(sam, string.Empty);
                }
                else
                    res = "<Response><Say voice=\"woman\">No valid option entered.</Say></Response>";
            }
            else
            {
                string[] pa =
                    sam.GetPredefinedAnswers(currentQuestion.ToString());

                foreach (string p in pa)
                {
                    string[] parts = p.Split('|');

                    if (parts[0].ToLower().Contains(val.ToLower()))
                    {
                        sam.InsertSurveyResponse("q" +
                            currentQuestion.ToString(), userId, parts[0]);

                        string nxtQ =
                            (currentQuestion < questions.Length) ?
                            "<Say voice=\"woman\">Please hold for the next question...</Say>" :
                            "<Say voice=\"woman\">The survey is complete. Thank you.</Say>";

                        if (currentQuestion < questions.Length)
                        {
                            res = "<Say voice=\"woman\">Answer... " +
                                parts[0][1] + " saved for question... " +
                                currentQuestion.ToString() + "</Say>" +
                                nxtQ;

                            res = ProcessQuestion(sam, res);
                            break;
                        }
                        else
                        {
                            res = "<Response>" + nxtQ + "</Response>";
                            break;
                        }
                    }
                    else
                    {
                        res = "<Response><Say voice=\"woman\">No valid answer entered.</Say></Response>";
                        break;
                    }
                }
            }
        }
    }
    return Response.AsText(res, "text/xml");
};
```

让我们对此进行分析，以了解正在发生的事情。

因为我们通过设置 questions 字符串数组为 null，currentQuestion 整数值为 0，userId 变量为空字符串来初始化状态，所以我们执行的第一项检查是验证 userId 是否确实为空。然后我们检查变量 val 是否包含至少两个字符的值（在此阶段，这代表在 /survey/incoming 端点输入的社会安全号码）。

我们希望知道变量 val 至少有两个字符，因为我们希望将其与其他响应区分开来，其他响应将是一个字符长，并代表对问题的答案。

当我们确信 val 确实是我们要求调用者输入的社会安全号码时，我们将 userId 变量的状态赋值给 val 变量的值。

如果 questions 字符串数组为 null，我们通过调用 SimpleAnsweringMachine 实例的 GetQuestions 方法从 Questions Azure 表中获取可用问题列表。

在可用问题列表准备好后，我们通过调用 ProcessQuestion 方法请求应用程序处理第一个问题。ProcessQuestion 方法是 AnsweringMachineMain NancyFX 模块的一个静态方法，我们稍后将进行探讨。

**ProcessQuestion** 方法的目的是让 Twilio 提出问题并描述可能的答案。然而，Twilio 并不处理对该问题的响应。对问题的实际响应是在 **ProcessQuestion** 方法调用 /survey/connect 端点时处理的。

本质上，/survey/connect 是自我重复的，这意味着为了提出多个问题并获取每个问题的答案，**ProcessQuestion** 方法会触发对执行该方法的同一端点的调用。这就是为什么维护状态很重要。

当第一个问题被提出后，下一次 /survey/incoming 被执行时（当处理对该问题的答案时），控制流传递到主要的 **else** 语句，该语句使代码通过调用 **SimpleAnsweringMachine** 实例的 **GetPredefinedAnswers** 方法获取所有可能的预定义答案。

从调用者接收到的答案，包含在 **val** 变量中，会被检查以确保它存在于从 PredefinedAnswers Azure 表检索到的预定义答案列表中。它通过调用 **GetPredefinedAnswers** 方法来实现这一点。

如果答案存在于正在被提问的当前问题的预定义答案列表中（正在被提问的当前问题是通过 **currentQuestion** 属性保持状态来获知的），该答案将通过调用 **InsertSurveyResponse** 方法与问题编号和 **userId** 一起存储在 ResponsesSuccinctly 表中。

如果提供了对问题的错误答案，即不属于正在被提问的当前问题的预定义答案列表中的答案，调查将被终止。此功能可以在未来得到改进，但目前已经足够好用。

当所有问题都被提出，答案被收集和处理后，可以在 Azure 上的 ResponsesSuccinctly 表上查看信息。

图 55 展示了完成的自动调查结果的样子（在使用 Visual Studio 发布应用程序并调用我们的 Twilio 号码后）。

![](img/7d3e41c7ef83c5fb4ef242998ad60317_104_0.png)

![](img/7d3e41c7ef83c5fb4ef242998ad60317_104_1.png)

让我们探索一下 **ProcessQuestion** 方法做什么。

