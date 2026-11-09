Developing an enterprise application is difficult because many months go into the effort. After the arduous development stage, though, you might go through a sequence of testing procedures only to find that the application bogs down under heavy loads.

The first thing that comes to mind in order to fix the problem is to give the servers substantial upgrades so that the application can handle the projected usage. But that is expensive in terms of hardware and network administration, and the servers will all have some down time. This is not what your client wants to hear.

If you're lucky, you'll easily find some performance-gaining steps you can take. You might even find something with a relatively small amount of investigation time. Some simple items such as changing from a File to a System DSN can make all the difference.

This scenario plays out in most software development shops at one time or another. A simple change can make an enormous difference in performance and save the day. Even more frustrating is the situation in which an application is deployed with great expectations, only to find that it can't handle heavy usage situations. This chapter addresses many of the Windows Distributed Internet Architecture (Windows DNA) performance issues, and shows you how to test your applications before you go live.

I'll start off with some Windows DNA performance topics, and give you some optimization techniques that you can apply right away. I'll also talk about using the Microsoft Windows DNA Performance Kit to benchmark your Windows DNA applications. Since COM+ is such a big part of Windows DNA, the DNA kit helps test your components within the Windows DNA framework.

# Assessing Your Needs

Before you dive headlong into the Windows DNA optimization morass, you need to ascertain your goal. It's possible that your application is ready even without any optimization. The most important hard number you'll need is the number of transactions per second (TPS) that the application must support. Two variables determine this: the application Think Time and the number of current users.

Think Time is the amount of human interaction time for each transaction. This includes reading and viewing screens, making decisions, and making selections or typing input. If your application is an order-entry system, the Think Time is the amount of time it takes for a user to view the catalog, decide what to buy, and select the desired items in the user interface.

To calculate the required TPS, divide the number of users by the Think Time as shown in the following formula: