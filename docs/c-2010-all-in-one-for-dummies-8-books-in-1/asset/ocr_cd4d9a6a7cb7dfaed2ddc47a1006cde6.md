# Making an ASMX Service 741

```
var conferenceQuery = from c in allConferences
where c.LocationID == locationID
select c;
List<Conference> locationConferences = conferenceQuery.ToList();
conferenceContext.Dispose();
```

```
return locationConferences;
```

{

# 5. To make it a service, you need to add the WebMethod decorator
no the method signature, and you are done.

```
[WebMethod]
public List<DbEntity> conferencesAtLocation(int locationID)
{
DbEntities conferenceContext = new DbEntities();
List<Conference> allConferences = conferenceContext.Conferences;
var conferenceQuery = from c in allConferences
where c.LocationID == locationID
select c;
List<Conference> locationConferences = conferenceQuery.ToList();
conferenceContext.Dispose();

return locationConferences;
```

{

# 6. Press F5 to run the test page, and click on the conferencesAtLocat tion method link. Enter 3 into the Test field, and the result shouldncome back like Figure 2-4 if everything is good.

So what about all that other stuff that goes SOAP? Security, transactions,
and like that? It's all baked in, but it's well within the scope of this book.

For instance, check the out the SoapHeader attribute. It allows you to specify
even the most complex security attributes on your Web methods. There's
more, too. Check out MSD.

![](bbox=[0.883, 0.513, 0.965, 0.65])

# Deploying

Deploying an XML Web Service is just like deploying a Web application. They
are effectively the same thing.

One benefit of ASMX over WCF is the simple configuration. In fact, if you
check out the configuration file for the application built here, you'll see
that the only configuration revolves around the Entity Model.
Adding an ASMX service to a Web project is easy.

Something you need to know: After you deploy, the sample
test page doesn't run anymore. You'll still get the information service page,
if you try to run the test script, you'll get the message shown in Figure
2-5. This is just for security and can be overridden, though I don't advise
overriding it in a production setting.

![](bbox=[0.133, 0.833, 0.193, 0.903])