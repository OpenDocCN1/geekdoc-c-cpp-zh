# Making an ASMX Service

# 5. To make it a service, you need to add the WebMethod decorator on the method signature, and you are done:

```
[WebMethod]
public List<Conference> conferencesAtLocation(int locationId)
{
    ConferenceDbEntities conferenceContext = new ConferenceDbEntities();
    DbSet<Conference> allConferences = conferenceContext.Conferences;
    var conferenceQuery = from c in allConferences
        where c.LocationId == locationId
        select
    List<Conference> locationConferences = conferenceQuery.ToList();
    conferenceContext.Dispose();

    return locationConferences;
}
```

# 6. Press F5 to run the test page and click the conferencesAtLocation method link; enter 3 into the field.

The result should come back like Figure 2-4, if everything is good.
So about all other stuff that goes into SOAP? Security, transactions, and like that? It's all baked in, but it's well beyond the scope of this.

For instance, check out the SoapHeader attribute. It allows you to specify even the most complex security attributes on your web methods. There's more, too. check out MSDN.

![](bbox=[0.235, 0.545, 0.839, 0.863])

Figure 2-4:
Results of the service.

Book VII
Chapter 2
Building Web Services with ASMX