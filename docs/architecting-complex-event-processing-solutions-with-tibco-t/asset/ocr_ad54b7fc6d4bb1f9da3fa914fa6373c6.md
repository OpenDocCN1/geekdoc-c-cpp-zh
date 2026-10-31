placed in a publishing table. The adapter periodically checks to see whether there are any entries in the publishing table and, if there are, publishes a message for each entry. If the inference agent is a subscriber to these messages, it will receive the notifications of database change and can take whatever actions are appropriate for the application.

# Database Interaction Using TIBCO ActiveMatrix BusinessWorks™

Using TIBCO ActiveMatrix BusinessWorks to perform the database interactions requires using a combination of two or three design patterns described earlier:

+   - TIBCO BusinessEvents as an Asynchronous Service Consumer
+   - ActiveMatrix BusinessWorks Receive Event
+   - ActiveMatrix BusinessWorks Send Event

Using the Asynchronous Service Consumer pattern, TIBCO BusinessEvents sends the request to ActiveMatrix BusinessWorks, which uses the ActiveMatrix BusinessWorks Receive Event pattern to start a process that will perform the database update(s) and perhaps other operations as well. Optionally, the process can employ the ActiveMatrix BusinessWorks Send Event pattern to report results back to TIBCO BusinessEvents.

The advantage of this pattern is that the full integration capabilities of ActiveMatrix BusinessWorks can be brought to bear. The database update can be performed as part of an XA transaction, and it can be coordinated with other activities as well.

# Summary

TIBCO BusinessEvents processing units can be deployed in TIBCO ActiveMatrix BusinessWorks engines. A palette of ActiveMatrix BusinessWorks activities enables ActiveMatrix BusinessWorks to interact with TIBCO BusinessEvents channels. ActiveMatrix BusinessWorks can use these activities to send events, wait for events, and invoke TIBCO BusinessEvents rule functions. There is also a process starter activity that can be used to define a process that can be started by TIBCO BusinessEvents sending a message.

TIBCO BusinessEvents can play the role of a service provider using a channel as the service interface. It can also play the role of a service