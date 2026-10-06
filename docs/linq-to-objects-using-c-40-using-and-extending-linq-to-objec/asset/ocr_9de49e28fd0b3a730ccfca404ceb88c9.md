# 38 CHAPTER 2 INTRODUCING LINQ TO OBJECTS

**Listing 2-13** Incoming log summary shows filtering, ordering, grouping, joining, and selection using aggregate values—see Output 2-8

```
List<Contact> contacts = Contact.SampleData();
List<CallLog> callLog = CallLog.SampleData();

var q = from call in callLog
    where call.Incoming == true
    group call by call.Number into g
    join contact in contacts on
        g.Key equals contact.Phone
    orderby contact.FirstName, contact.LastName
    select new {
        contact.FirstName,
        contact.LastName,
        Count = g.Count(),
        Avg = g.Average(c => c.Duration),
        Total = g.Sum(c => c.Duration));
```

```
foreach (var call in q)
    Console.WriteLine("{0} {1} - Calls:{2}, Time:{3}mins, Avg:{4}mins*",
    call.FirstName, call.LastName,
    call.Count, call.Total, Math.Round(call.Avg, 2));
```

# Output 2-8

Ariel Hazelgrove - Calls:2, Time:27mins, Avg:13.5mins
Armando Valdes - Calls:2, Time:20mins, Avg:10mins
Barney Gottshall - Calls:4, Time:31mins, Avg:7.75mins
Chance Lard - Calls:2, Time:22mins, Avg:11mins
Mack Kamph - Calls:2, Time:44mins, Avg:22mins
Stewart Kagel - Calls:2, Time:13mins, Avg:6.5mins