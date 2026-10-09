```
```
int tMin = DateTime.Now.Minute;
int tSec = DateTime.Now.Second;

DateTime tdy = new DateTime(tYear, tMonth, tDay, tHour,
	Min, tSec);

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
	int year = Convert.ToInt32(en.Time.Substring(4, 2));
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
catch (Exception ex)
{
	Console.WriteLine(ex.ToString());
}

return res;

public bool MarkAsSent(AppointmentData ad)
{
	bool res = false;
```
```