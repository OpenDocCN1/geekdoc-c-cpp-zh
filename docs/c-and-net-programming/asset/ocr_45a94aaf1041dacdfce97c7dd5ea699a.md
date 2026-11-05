+   - StateServer
+   - SQLServer
+   - Custom
+   - Off

By default, the Session state mode is InProc means Session state is stored in memory in the same process as the ASP.NET process. So accessing data is very fast. Another advantage is that there are no requirements of serialization to store data in InProc Session Mode.

| Session State Mode | State Provider |
|---|---|
| InProc | In-Memory Object |
| StateServer | Aspnet_state.exe |
| SQLServer | DataBase |
| Custom | CustomProvider |

In server side state management, all the information is stored in the user memory. Due to this functionality, there are more secure domains at server side in comparison to client side state management.

Session state and application state at a glance,

| Application | Session |
|---|---|
| It works at application level rather than user level. | Session object is user specific. |
| Application state is stored only in the memory on the server. | Session state is stored in inProc and outProc |
| Application state does not depends upon client's cookies | Session object depends upon cookie or can be cookieless. |
| Application state does not depend upon the current browser. | Session state has scope to the current browser only. |

# **Q.9 Name the benefits provided by XML classes in .NET.**

**AU: Dec.-18**

**Ans. :** The .NET Framework provides a comprehensive and integrated set of classes that enable to build XML-aware apps easily. The classes in the following namespaces support parsing and writing XML, editing XML data in memory, data validation, and XSLT transformation.

+   - System.Xml