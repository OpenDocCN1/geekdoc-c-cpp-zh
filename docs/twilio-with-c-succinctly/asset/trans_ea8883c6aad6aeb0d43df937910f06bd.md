

若要安装 NuGet 包，只需单击“安装”。这将把必要的引用添加到 Visual Studio 项目中。

在深入代码之前，你需要使用 Azure Storage Explorer 创建存储表。让我们将该表命名为 `AppointmentsSuccinctly`。

安装了 NuGet 包后，我们可以创建 `AppointmentData` 和 `Appointment` 类。

### 代码清单 14：Appointment 和 AppointmentData 类

```csharp
using System;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Table;

namespace TwilioSuccinctly
{
    public class AppointmentData : TableEntity
    {
        public AppointmentData(string p, string d)
        {
            PartitionKey = p;
            RowKey = d;
        }

        public AppointmentData()
        {
        }

        public string Id { get; set; }
        public string Name { get; set; }
        public string PhoneNumber { get; set; }
        public string Time { get; set; }
        public bool Sent { get; set; }
    }

    public class Appointment : IDisposable
    {
        private const string cStrConnStr = "<< Your Azure Storage Connection String >>";
        private const string cStrAppTable = "AppointmentsSuccinctly";

        protected bool disposed;

        public AppointmentData Data { get; set; }

        public Appointment(string id, string n, string pn, DateTime t)
        {
            string tt = t.Day.ToString().PadLeft(2, '0') +
                        t.Month.ToString().PadLeft(2, '0') +
                        t.Year.ToString() +
                        t.Hour.ToString().PadLeft(2, '0') +
                        t.Minute.ToString().PadLeft(2, '0') +
                        t.Second.ToString().PadLeft(2, '0');

            Data = new AppointmentData(pn, tt);

            Data.Sent = false;
            Data.Id = id;
            Data.Name = n;
            Data.PhoneNumber = pn;
            Data.Time = tt;
        }

        public Appointment(string pn)
        {
            string tt = DateTime.Now.Day.ToString().PadLeft(2, '0') +
                        DateTime.Now.Month.ToString().PadLeft(2, '0') +
                        DateTime.Now.Year.ToString() +
                        DateTime.Now.Hour.ToString().PadLeft(2, '0') +
                        DateTime.Now.Minute.ToString().PadLeft(2, '0') +
                        DateTime.Now.Second.ToString().PadLeft(2, '0');

            Data = new AppointmentData(pn, tt);
            Data.PhoneNumber = pn;
            Data.Time = tt;
        }

        ~Appointment()
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

                Data = null;
            }
            disposed = true;
        }

        public void Dispose()
        {
            Dispose(true);
            GC.SuppressFinalize(this);
        }

        public bool Create()
        {
            bool res = false;

            try
            {
                var storageAccount = CloudStorageAccount.Parse(cStrConnStr);

                CloudTableClient tableClient =
                    storageAccount.CreateCloudTableClient();
                CloudTable table =
                    tableClient.GetTableReference(cStrAppTable);

                TableOperation retrieveOperation =
                    TableOperation.Retrieve<AppointmentData>
                    (Data.PhoneNumber, Data.PhoneNumber);

                TableResult retrievedResult =
                    table.Execute(retrieveOperation);
                AppointmentData updateEntity =
                    (AppointmentData)retrievedResult.Result;

                if (updateEntity == null)
                {
                    updateEntity = new AppointmentData(Data.PhoneNumber,
                        Data.Time);
                    updateEntity.Id = Data.Id;
                    updateEntity.Name = Data.Name;
                    updateEntity.PhoneNumber = Data.PhoneNumber;
                    updateEntity.Time = Data.Time;
                }

                TableOperation ins = TableOperation.Insert(updateEntity);
                table.Execute(ins);

                res = true;
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.ToString());
            }

            return res;
        }

        public AppointmentData Get()
        {
            AppointmentData res = null;

            try
            {
                int tDay = DateTime.Now.Day;
                int tMonth = DateTime.Now.Month;
                int tYear = DateTime.Now.Year;
                int tHour = DateTime.Now.Hour;
                int tMin = DateTime.Now.Minute;
                int tSec = DateTime.Now.Second;

                DateTime tdy = new DateTime(tYear, tMonth, tDay, tHour,
                    tMin, tSec);

                var storageAccount =
                    CloudStorageAccount.Parse(cStrConnStr);
                CloudTableClient tableClient =
                    storageAccount.CreateCloudTableClient();
                CloudTable table =
                    tableClient.GetTableReference(cStrAppTable);

                TableQuery<AppointmentData> query = new
                    TableQuery<AppointmentData>().Where(
                    TableQuery.GenerateFilterCondition("PartitionKey",
                        QueryComparisons.Equal, Data.PhoneNumber));

                foreach (AppointmentData en in table.ExecuteQuery(query))
                {
                    int day = Convert.ToInt32(en.Time.Substring(0, 2));
                    int month = Convert.ToInt32(en.Time.Substring(2, 2));
                    int year = Convert.ToInt32(en.Time.Substring(4, 4));
                    int hour = Convert.ToInt32(en.Time.Substring(8, 2));
                    int min = Convert.ToInt32(en.Time.Substring(10, 2));
                    int sec = Convert.ToInt32(en.Time.Substring(12, 2));

                    DateTime exp = new DateTime(year, month, day, hour,
                        min, sec);

                    if (!en.Sent && DateTime.Compare(tdy, exp) >= 0)
                    {
                        res = en;
                        break;
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.ToString());
            }

            return res;
        }

        public bool MarkAsSent(AppointmentData ad)
        {
            bool res = false;

            try
            {
                var storageAccount =
                    CloudStorageAccount.Parse(cStrConnStr);
                CloudTableClient tableClient =
                    storageAccount.CreateCloudTableClient();

                CloudTable table =
                    tableClient.GetTableReference(cStrAppTable);

                TableOperation retrieveOperation =
                    TableOperation.Retrieve<AppointmentData>
                    (ad.PhoneNumber, ad.Time);

                TableResult retrievedResult =
                    table.Execute(retrieveOperation);
                AppointmentData updateEntity =
                    (AppointmentData)retrievedResult.Result;

                if (updateEntity != null)
                {
                    updateEntity.Sent = ad.Sent;

                    TableOperation insertOrReplaceOperation =
                        TableOperation.InsertOrReplace(updateEntity);
                    table.Execute(insertOrReplaceOperation);

                    res = true;
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.ToString());
            }

            return res;
        }

        public string FormatTime(string t)
        {
            int day = Convert.ToInt32(t.Substring(0, 2));
            int month = Convert.ToInt32(t.Substring(2, 2));
            int year = Convert.ToInt32(t.Substring(4, 4));
            int hour = Convert.ToInt32(t.Substring(8, 2));
            int min = Convert.ToInt32(t.Substring(10, 2));
            int sec = Convert.ToInt32(t.Substring(12, 2));

            DateTime exp = new DateTime(year, month, day, hour, min,
                sec);
            return exp.ToString();
        }
    }
}
```

让我们分析这段代码。我们定义了一个 **AppointmentData** 类，它表示要存储在 Azure 表存储中的数据。**AppointmentData** 类继承自 **TableEntity**，并包含表存储用于索引和查找数据记录的 **PartitionKey** 和 **RowKey** 属性。

我们将把用户的电话号码存储在 **PartitionKey** 上，而在 **RowKey** 上，我们将以字符串形式保留预约到期时的日期和时间，例如，29042016203000，其中 29 是日，04 是月，2016 是年，20 是一天中的小时（晚上 8 点），30 是分，00 是秒。

**AppointmentData** 类还包含一个 **string Id** 属性，一个表示预约名称的 **string Name** 属性，一个包含与 **PartitionKey** 相同数据的 **string PhoneNumber** 属性，一个包含与 **RowKey** 相同数据的 **string Time** 属性，以及一个表示是否已为该预约发送短信的 **bool Sent** 属性。

**AppointmentData** 类将由 **Appointment** 类实例化，以便将信息存储在 Azure 表存储中。你可以将 **AppointmentData** 类视为数据层（模型），将 **Appointment** 类视为业务逻辑层（控制器）。

**Appointment** 类的构造函数创建一个 **AppointmentData** 实例，该实例将用于在 Azure 上存储预约数据。

在表存储中，**DateTime** 值应以 *string* 值的形式存储。**FormatTime** 方法的目的接收像 29042016203000 这样的日期时间 *string*，并将其转换为等效的 *DateTime* 表示形式（4/29/2016 8:30:00 PM），作为 *string*，以便可以在 **Console** 上显示。

**Create** 方法负责在表存储中创建预约提醒。通过将 **cStrConnStr** 连接字符串传递给 **CloudStorageAccount.Parse** 方法，建立与 Azure 实例的连接。接下来，创建 **CloudTableClient** 的实例，然后使用它获取 AppointmentsSuccinctly 表的引用。

调用 **CloudTable** 实例的 **Execute** 方法，并使用 **AppointmentData** 类作为 T，**Data.PhoneNumber** 作为 **PartitionKey** 和 **RowKey**。我们这样做是为了获取一个 *TableResult* 对象，以便可以将其 **Result** 属性强制转换为空的 **AppointmentData** 对象。该对象将用于设置相应的预约属性，并通过调用 **TableOperation.Insert** 方法插入到表存储中。最后，**CloudTable** 实例的 **Execute** 方法将 **AppointmentData** 对象提交到表存储。

![Image](img/7d3e41c7ef83c5fb4ef242998ad60317_43_0.png)
![Image](img/7d3e41c7ef83c5fb4ef242998ad60317_43_1.png)

