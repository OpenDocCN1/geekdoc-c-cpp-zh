

```csharp
    tableClient.GetTableReference(cStrSurveyQuestions);   

    TableQuery<QuestionsData> query = new
        TableQuery<QuestionsData>().Where(
        TableQuery.GenerateFilterCondition("PartitionKey", 
        QueryComparisons.NotEqual, "-1"));

    foreach (QuestionsData en in table.ExecuteQuery(query))
    {
        {   
            q.Add(en.Question);
        }
    }
    catch (Exception ex)
    {
        Console.WriteLine(ex.ToString());
    }

    return q.ToArray();
}
```

让我们快速检查一下这段逻辑。

由于我们希望检索存储在 Questions 表中的所有问题，我们只需查询所有 **PartitionKey** 不等于 -1 的记录，这意味着将返回所有记录（因为我们在通过 Azure Storage Explorer 创建该表时，没有为 **PartitionKey** 等于 -1 输入任何记录）。

与 Questions 一样，我们还需要为 PredefinedAnswers 和 ResponsesSuccinctly 分别定义一个类。我们将这些类分别命名为 **PredefinedAnswersData** 和 **RespondeData**。让我们现在通过代码列表 42 来完成这一操作。

### 代码列表 42：PredefinedAnswersData 和 RespondeData 类

```csharp
public class PredefinedAnswersData : TableEntity   
{
    public PredefinedAnswersData(string p, string d)
    {
        PartitionKey = p;
        RowKey = d;
    }

    public PredefinedAnswersData()
    {
    }

    public string Answer { get; set; }
}
```

```csharp
public class ResponseData : TableEntity
{
    public ResponseData(string p, string d)
    {
        PartitionKey = p;
        RowKey = d;
    }

    public ResponseData()
    {
    }

    public string Response { get; set; }
}
```

接下来，我们在 SimpleAnsweringMachine 类中实现一个方法来从 PredefinedAnswers 表中检索记录，我们将该方法命名为 GetPredefinedAnswers。

### 代码列表 43：GetPredefinedAnswers 方法

```csharp
public string[] GetPredefinedAnswers(string qn)
{
    List<string> pa = new List<string>();

    try
    {
        var storageAccount = CloudStorageAccount.Parse(cStrConnStr);
        CloudTableClient tableClient =
            storageAccount.CreateCloudTableClient();
        CloudTable table =
            tableClient.GetTableReference(cStrSurveyAnswers);

        TableQuery<PredefinedAnswersData> query = new
            TableQuery<PredefinedAnswersData>().Where(
                TableQuery.GenerateFilterCondition("RowKey",
                    QueryComparisons.Equal, "q" + qn));

        foreach (PredefinedAnswersData en in table.ExecuteQuery(query))
        {
            pa.Add(en.PartitionKey + "|" + en.Answer);
        }
    }
    catch (Exception ex)
    {
        Console.WriteLine(ex.ToString());
    }
    
    return pa.ToArray();
}
```

该方法通过 RowKey 查询 PredefinedAnswers 表，查找与调用者所问问题相匹配的记录。然后，这些答案以字符串数组的形式返回，以便进一步处理。

现在，让我们创建一个方法来填充 ResponsesSuccinctly 表。我们也将此方法添加到代码列表 44 中的 SimpleAnsweringMachine 类中。

### 代码列表 44：InsertSurveyResponse 方法

```csharp
public void InsertSurveyResponse(string qId, string uId, string aId)
{
    try
    {
        var storageAccount = CloudStorageAccount.Parse(cStrConnStr);
        CloudTableClient tableClient =
            storageAccount.CreateCloudTableClient();
        CloudTable table =
            tableClient.GetTableReference(cStrSurveyResponses);

        TableOperation retrieveOperation =
            TableOperation.Retrieve<ResponseData>(qId, uId);

        TableResult retrievedResult = table.Execute(retrieveOperation);
        ResponseData updateEntity = (ResponseData)retrievedResult.Result;
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
```

观察这个方法，我们可以看到 **ResponseSuccinctly** 表通过问题 ID (**qId**) 作为 **PartitionKey** 和用户 ID (**uId**) 作为 **RowKey** 进行查询。

如果未找到记录（**updateEntity** 为 **null**），则会为 **updateEntity** 的属性赋值，并通过调用 **Execute** 方法将此对象插入到表中。

现在，让我们查看我们的 **SimpleAnsweringMachine** 类和 .cs 文件的完整更新代码。

### 代码列表 45：更新后的 SimpleAnsweringMachine.cs 文件

```csharp
using System;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Table;
using System.Collections.Generic;

namespace TwilioSuccinctly
{
    public class SimpleAnsweringMachineData : TableEntity
    {
        public SimpleAnsweringMachineData(string p, string d)
        {
            PartitionKey = p;
            RowKey = d;
        }

        public SimpleAnsweringMachineData()
        {
        }
    }

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

    public class PredefinedAnswersData : TableEntity
    {
        public PredefinedAnswersData(string p, string d)
        {
            PartitionKey = p;
            RowKey = d;
        }
        public PredefinedAnswersData()
        {
        }

        public string Answer { get; set; }
    }

    public class ResponseData : TableEntity
    {
        public ResponseData(string p, string d)
        {
            PartitionKey = p;
            RowKey = d;
        }

        public ResponseData()
        {
        }

        public string Response { get; set; }
    }

    public class SimpleAnsweringMachine : IDisposable
    {
        #region "private declarations"
        protected bool disposed;

        private const string cStrConnStr =
            "<< Your Azure Storage Connection String >>";
        private const string cStrAppTable = "SAM Succinctly";
        private const string cStrSurveyResponses = "ResponsesSuccinctly";
        private const string cStrSurveyQuestions = "Questions";
        private const string cStrSurveyAnswers = "PredefinedAnswers";

        public SimpleAnsweringMachine()
        {
        }

        ~SimpleAnsweringMachine()
        {
            Dispose(false);
        }

        public virtual void Dispose(bool disposing)
        {
            if (!disposed)
            {
                if (disposing)
                {
                }
            }

            disposed = true;
        }

        public void Dispose()
        {
            Dispose(true);
            GC.SuppressFinalize(this);
        }

        public string Get(string ac)
        {
            string res = string.Empty;

            try
            {
                var storageAccount =
                    CloudStorageAccount.Parse(cStrConnStr);
                CloudTableClient tableClient =
                    storageAccount.CreateCloudTableClient();
                CloudTable table =
                    tableClient.GetTableReference(cStrAppTable);

                TableQuery<SimpleAnsweringMachineData> query = new
                    TableQuery<SimpleAnsweringMachineData>().Where(
                        TableQuery.GenerateFilterCondition("PartitionKey",
                            QueryComparisons.Equal, ac));

                foreach (SimpleAnsweringMachineData en in
                    table.ExecuteQuery(query))
                {
                    res = en.RowKey;
                    break;
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.ToString());
            }

            return (res == string.Empty) ? "Unknown" : res;
        }

        public string[] GetQuestions() 
        { 
            List<string> q = new List<string>(); 
            try 
            { 
                var storageAccount = 
                    CloudStorageAccount.Parse(cStrConnStr); 
                CloudTableClient tableClient = 
                    storageAccount.CreateCloudTableClient(); 
                CloudTable table = 
                    tableClient.GetTableReference(cStrSurveyQuestions); 

                TableQuery<QuestionsData> query = new 
                    TableQuery<QuestionsData>().Where(
                        TableQuery.GenerateFilterCondition("PartitionKey", 
                        QueryComparisons.NotEqual, "-1")); 

                foreach (QuestionsData en in table.ExecuteQuery(query)) 
                { 
                    q.Add(en.Question); 
                }
            }
            catch (Exception ex) 
            { 
                Console.WriteLine(ex.ToString()); 
            }
            return q.ToArray(); 
        }

        public string[] GetPreDefinedAnswers(string qn) 
        { 
            List<string> pa = new List<string>(); 
            try 
            { 
                var storageAccount = 
                    CloudStorageAccount.Parse(cStrConnStr); 
                CloudTableClient tableClient = 
                    storageAccount.CreateCloudTableClient(); 
                CloudTable table = 
                    tableClient.GetTableReference(cStrSurveyAnswers); 

                TableQuery<PreDefinedAnswersData> query = new 
                    TableQuery<PreDefinedAnswersData>().Where(
```

