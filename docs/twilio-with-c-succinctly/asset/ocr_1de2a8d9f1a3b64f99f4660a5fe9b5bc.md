```
public LeadsData Get(string webinar)
{
    LeadsData res = null;

    try
    {
        int tDay = DateTime.Now.Day;
        int tMonth = DateTime.Now.Month;
        int tYear = DateTime.Now.Year;
        int tHour = DateTime.Now.Hour;
        int tMin = DateTime.Now.Minute;
        int tSec = DateTime.Now.Second;

        DateTime tdy = new DateTime
            (tYear, tMonth, tDay, tHour, tMin, tSec);

        var storageAccount =
            CloudStorageAccount.Parse(cStrConnStr);
        CloudTableClient tableClient =
            storageAccount.CreateCloudTableClient();
        CloudTable table =
            tableClient.GetTableReference(cStrAppTable);

        TableQuery<LeadsData> query = new
            TableQuery<LeadsData>().Where(
            TableQuery.GenerateFilterCondition("PartitionKey",
            QueryComparisons.Equal, webinar));

        foreach (LeadsData en in table.ExecuteQuery(query))
        {
            int day = Convert.ToInt32(
                en.RowKey.Substring(0, 2));
            int month = Convert.ToInt32(
                en.RowKey.Substring(2, 2));
            int year = Convert.ToInt32(
                en.RowKey.Substring(4, 4));
            int hour = Convert.ToInt32(
                en.RowKey.Substring(8, 2));
            int min = Convert.ToInt32(
                en.RowKey.Substring(10, 2));
            int sec = Convert.ToInt32(
                en.RowKey.Substring(12, 2));

            DateTime exp = new DateTime(
                year, month, day, hour, min, sec);

            if (!en.FollowedUp &&
```