# 19.9 WebSockets (ABAP Channels and Messages)

Say you have an ALV report that displays up-to-date sales data. This report fetches the sales data from the database and displays it as a report output. While you're looking at the report output, if any new sales are entered in the system, those new sales won't appear in the report.

Because the data was fetched when the report was executed, you'll only see the current data as of the time of the report was run. What if you want the report to always display up-to-date sales data, even if you spend an hour going through the report output? One way of doing this is to refresh the report frequently or use the `CL_GUI_TIMER` class to auto-refresh the report. However, this approach will put an unnecessary load on the database, because the report will be frequently refreshed (polling) to look for new data even when none is available.

ABAP channels enable event-driven communication and implement a publish/subscribe mechanism. The ABAP messaging channel acts as a broker for the message exchange between ABAP sessions in different application servers. Any ABAP session can subscribe to channels, and any ABAP session can publish messages through channels.

What if there was a mechanism through which the report could be informed to refresh as soon as data is updated in the database? This is where ABAP channels and messages come into the picture. Using ABAP channels, the program that updates the data can act as a producer and raise a message to which the report can subscribe as a subscriber.

ABAP channels come in two flavors:

+   - **ABAP messaging channels**\n  Designed to send messages between programs running on different application servers\n- **ABAP push channels**\n  Designed to send messages to and from the Internet using WebSockets

You can create ABAP messaging channels and push channels in Object Navigator via the context menu path **CREATE • CONNECTIVITY**. ABAP push channels are used in web applications such as Web Dynpro ABAP, SAPUI5, and more; a discussion of ABAP push channels is beyond the scope of this book. In this section,