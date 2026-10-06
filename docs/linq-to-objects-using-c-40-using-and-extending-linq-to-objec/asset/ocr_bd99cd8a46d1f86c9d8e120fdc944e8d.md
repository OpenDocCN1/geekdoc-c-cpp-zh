# CHAPTER 1 INTRODUCING LINQ

```
// join calls with contacts data
foreach (Contact con in contacts)
{
    if (callGroups.ContainsKey(con.Phone))
    {
        List<CallLog> calls = callGroups[con.Phone];

        // calculate the total call duration and average
        long sum = 0;
        foreach (CallLog call in calls)
            sum += call.Duration;

        double avg = (double)sum / (double)calls.Count;

        // write XML record for this contact
        doc.WriteStartElement("contact");

        doc.WriteElementString("lastName",
            con.LastName);
        doc.WriteElementString("firstName",
            con.FirstName);
        doc.WriteElementString("count",
            calls.Count.ToString());
        doc.WriteElementString("totalDuration",
            sum.ToString());
        doc.WriteElementString("averageDuration",
            avg.ToString());

        doc.WriteEndElement();
    }
}
doc.WriteEndElement();
doc.Flush();
doc.Close();

Console.WriteLine(writer.ToString());
```

# LINQ Approach

LINQ to Objects and the new XML programming interface included in C# 3.0 (LINQ to XML, but this example uses the generation side of this API