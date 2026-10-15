# Introducing the Phone Execution Model

When you are using your desktop computer, you can interact with application processes in a variety of ways. Typically, you launch an application process, interact with the application, and then shut the application down. With today’s modern computers and operating systems, people usually launch multiple applications and leave them all running until they shut the computer down. On today’s laptops, many people don’t even bother shutting their computer down anymore—they just close the lid and open the lid again the next time they want to resume their work. They expect everything to appear as it last was when they shut the lid.

The idea that all your applications are running on your computer and are available by clicking the window or using a hot key (such as Alt+Tab on Windows) is nothing new. In fact, it is so prevalent that people expect applications to look exactly as they left them when they lost focus.

This particular model doesn’t work on mobile phones. Mobile devices have limited memory and CPU resources and cannot leave a bunch of applications running at the same time. In fact, Windows Phone 7 allows only a single application to be running at any given time.

Just because the phone is limited to one active application at a time doesn’t mean the user can’t get a rich experience in which applications remember what they were doing at the time the user launched a different application. Applications can save transient state, such as what a user had typed into a textbox when a new application was launched, and they can save persistent state that, as the name implies, persists between multiple launches.

This is where the application life cycle comes in. Windows Phone 7 applications are given fair warning when pages are about to be navigated away from, when the application was launched as a fresh instance, or when it was reactivated from a previously suspended (tombstoned) instance, when an application is going to be deactivated as a result of some other application (such as a phone call) moving to the foreground.

This next section takes you on a tour of all the various stages and events in the life cycle of a Windows Phone 7 application. When you are done reading this section, you should have a thorough understanding of how WP7 compensates for the one-application limitation and how, if your application is written properly, end users will never even notice this limitation.

# Application Life Cycle Walkthrough

Unlike desktop applications that can be started only by launching a brand new instance, Windows Phone 7 applications have multiple entry and exit points, and each of those implies a different impact on the application, its running state, and the data the application is holding in memory. The following sections describe the various stages in the life-time of a Windows Phone 7 application and how users typically get into and out of those stages. Figure 13.1 shows an example of transitions between the various stages of the WP7 application life cycle.