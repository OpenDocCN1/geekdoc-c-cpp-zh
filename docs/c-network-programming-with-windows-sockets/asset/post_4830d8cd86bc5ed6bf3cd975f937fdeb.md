
![](img/5e551abe6e0cb0588043ee757a235ddb_6_0.png)

Modem access can also operate in the opposite direction. It’s possible to have remote users dial into the computer network. Once they’re logged on to the network, the remote users have the same access to network resources as users whose computers are physically attached to the network. Microsoft’s Remote Access Service (RAS) includes this capability for Windows for Workgroups and Windows NT.

## Compute Servers

Another shared resource that can be found attached to some PC networks is the compute server. This device is usually a very powerful computer that’s geared toward performing specialized tasks. For example, compute servers can be tuned for exceptional floating-point calculation performance. A compute server isn’t necessarily practical for use as a general-purpose computer, so users access this resource from a workstation or desktop PC. The results of the compute server’s work can be displayed on the local desktop PC using a remote graphical user interface. This graphical interface is based on the X Window System developed at the Massachusetts Institute of Technology.

Another way to take advantage of a compute server is to use Remote Procedure Calls (RPC) in your desktop application. Using RPCs, the application on the desktop computer makes calls to functions that happen to execute on the remote compute server. When the function has completed, the results are returned to the desktop computer as if the function call took place locally. Figure 1.3 shows one possible scenario with a powerful mainframe compute server serving the needs of both an X Window workstation and a PC using RPCs.

![](img/5e551abe6e0cb0588043ee757a235ddb_7_0.png)

## Database Servers

The networked database server is similar to the compute server but is more common in today’s business environment. With this network resource, desktop PCs can query and modify a database that’s made available to the entire enterprise. Figure 1.4A shows one possible configuration. The user seated at the client computer sends a query to the database server. The database server receives the query parameters and processes the request. When the database server has completed the necessary processing, a response is returned to the client computer. This configuration is known as the client/server architecture. The client/server programming model is explained later in this chapter.

Several vendors, including Microsoft, Oracle, and Sybase, provide database servers that are geared toward the high-end client/server market. Many companies, such as Borland, Gupta, Microsoft, PowerSoft, and Oracle, provide tools necessary to build the client portion of the client/server solution.

A client/server database is especially useful when several people need access to the same information. This architecture is desirable because it allows people in different locations, possibly even on opposite sides of the globe, to share and modify common information. The client/server database architecture not only makes it easy to locate users at disparate locations but also allows freedom in the location of the databases. With this scenario, as shown in Figure 1.4B, the database can be maintained where it makes the most sense. In an order entry system, for example, it might make sense to have the billing department maintain the customer records in one database while the inventory records are maintained by the parts department in a different database stored on another database server. During order entry time, the order entry clerk can access both databases and get the most up-to-date information.

![](img/5e551abe6e0cb0588043ee757a235ddb_8_0.png)

## Communications Medium

The complementary, and somewhat overlapping, goal for a computer network is to act as a communications medium. In a basic sense, if this communications medium didn’t exist, neither would the ability to share any network resources, as described earlier. In this context, however, the communications medium allows network users to communicate better with each other. To facilitate this human-to-human communication, many networked software tools have been built. Among them are electronic mail systems, workgroup scheduling programs, and electronic forms processing systems.

**FIGURE 1.4B.** *Departmental database servers.*

![](img/5e551abe6e0cb0588043ee757a235ddb_9_0.png)

### Electronic Mail

Electronic mail, known as *e-mail*, has wide acceptance in the arena of larger computer systems such as those that run a UNIX operating system derivative. PC networks now have e-mail capability, too. Not only can e-mail be shared between PC network users, but it can be routed to users on other networks that are based on high-end workstations or multiuser computers. This capability means that all computer users in a business setting can use electronic communications among themselves and can still use the best computer and operating system combination to meet their primary job responsibilities.

Modern e-mail systems have been extended further so that embedded or attached objects can be sent. These objects can be as simple as additional textual information or as diverse as a computer-playable video presentation or a financial spreadsheet. When recipients read their e-mail, the attachments are immediately available.

Windows for Workgroups and Windows NT are bundled with e-mail support.

### Electronic Forms

With electronic forms an organization can easily exchange structured information. E-forms are the modern-day equivalent of the printed paper form. A simple example of a form is the popular “While You Were Out” message your secretary might fill out. By combining e-forms with an e-mail system, your messages will appear as nicely formatted, standardized e-mail messages instead of pieces of paper scattered about your desk. Another use of an e-form might be by a salesman who enters a customer’s order on his laptop computer while on site. The e-form is then either immediately transferred to a host computer using a modem or transferred at the end of the business day in a batch-type mode where all the day’s orders are sent.

### Workgroup Scheduling

Workgroup scheduling helps coworkers manage their time and communicate with each other more effectively. A network scheduling program provides network computer users with the ability to view and modify each other’s day planners. This ability makes it easier to schedule group meetings, make personal appointments, and assign tasks to an available individual. Microsoft’s Windows for Workgroups and Windows NT include a scheduling program that has this capability.

### Chat

A chat utility can replace a phone call for simple one-to-one or one-to-many communications. Under a UNIX-based operating system, the chat utility is called talk. In the Windows and Windows NT environment, the chat utility is called Chat and is executed by running the WINCHAT.EXE program. With both programs you can connect to at least one other network user and then type messages back and forth.

### World Wide Web and Mosaic

On a more global scale, the World Wide Web (WWW) is gaining in popularity. The WWW was started at CERN, the European Laboratory for Particle Physics. Its original purpose was to facilitate the communication between fellow particle physicists. WWW is a distributed system with which users can access documents of varying types, from simple text files to graphical images stored in the GIF or JPEG format. The data may contain links to other related data. By traversing these links, information on a particular topic can be found. This world-wide connection is made possible by the Internet, a collection of an estimated 2,000,000 interconnected computer systems spread the world over.

To traverse the Web, as it is known, the user needs a sophisticated Web client or browser. The browser’s duties involve traversing the links, retrieving data of miscellaneous types, and providing viewers for that data. One of the best Web browsers available is Mosaic, developed at the National Center for Supercomputing Applications. Figure 1.5 shows Mosaic for Windows connected to a computer that Microsoft has made available for support of its products. Pointing the mouse cursor at the folder and clicking the mouse button causes Mosaic to redraw the screen with the newly selected folder’s information. When users see data files they would like, another mouse click causes files to be retrieved to the users’ machines where they’re displayed, if there are appropriate viewers available, or saved to disk for later examination.

Webs are even finding a place for internal use in the corporation. The data stored at a Web site is inherently cross-platform. This means a company can produce a document once, possibly including multimedia-type extensions, and have that document available for viewing by users of Windows, Macintosh, or UNIX computers. All that is needed is a Web browser for each platform.

**FIGURE 1.5.** *Mosaic.*

![](img/5e551abe6e0cb0588043ee757a235ddb_11_0.png)
