With this controller in place, it is already possible to do first tests from the browser. Opening the link http://localhost:5000/api/BookChapters returns JSON.

Port 5000 is the default port number when using the Kestrel web server. You can select this server in the Debug section of the project properties (see Figure 42.2) by choosing the Web profile.

![](bbox=[0.105, 0.209, 0.894, 0.568])

# Figure 42.2

When you open this link in a browser, a JSON array is returned as shown:

```
[{"Id":"2d0c7eac-cb37-409f-b8da-c8ca497423a2","Number":6,"Title":"Generics","Pages":22},
{"Id":"d62e1182-3254-4504-a56b-f0441ee1ce8e","Number":1,"Title":"Application Architectures","Pages":35},
{"Id":"cb624eed-7e6c-40c6-88f2-28cf03eb652e","Number":4,"Title":"Inheritance","Pages":18},
{"Id":"6e6d48b5-fa04-43b5-b5f5-acd11b72c821","Number":3,"Title":"Objects and Types","Pages":30},
{"Id":"55c1ea93-2c0d-4071-8cee-cc172b3746b5","Number":2,"Title":"Core C#","Pages":42},
{"Id":"5c391b33-76f3-4e12-8989-3a8fbc621e96","Number":5,"Title":"Managed and Unmanaged Resources","Pages":20}]
```

# Changing the Response Format

ASP.NET Web API 2 returned JSON or XML, depending on the requested format by the client. With ASP.NET MVC 6, when returning an ObjectResult, by default JSON is returned. In case you need to