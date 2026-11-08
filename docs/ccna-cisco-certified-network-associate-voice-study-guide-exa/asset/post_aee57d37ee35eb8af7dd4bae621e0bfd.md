
and again until you locate the source of the problem. Once the problem source is located, it should be documented. You may also want to go back to your baseline and make necessary changes to prevent the problem from recurring. However, the main focus of this discussion is on research, and the act of documenting your solution will be helpful to you and any other administrator who faces the same or similar problem. Documentation is discussed more in the later section called “Take Note,” but know that your organization’s internal database of problem solutions will be one of the most valuable sources you build over time.

At the end of the Research phase, I may have a solution to my problem. If that is the case, I will resolve the problem and move to the final phase so that I can document the problem and solution for future reference. If my research has only given me direction or has yielded no results after a few minutes, I will move on to the next phase: Engage.

## Engage

While you may be eager to move from the Research phase to the Adjust phase, you should engage the user if he or she is involved in the problem. Avoid the temptation of jumping right in and making changes. You may engage the user before researching the problem, or you may only gather summary information about the problem before doing the research. Either way, these first two phases are essential, and you may find yourself in a reciprocal process alternating between researching and engaging for some time.

When you engage the user, ask a question like, “Do you know if anything has changed about your system in the past few days?” Notice I didn’t say, “Did you change anything?” The latter question will usually cause people to become defensive and will fail to get you any valuable information. The users do not usually have any knowledge of what caused the problem, but when they do, it can save you hours or even days of trouble. Always engage the user. Other questions that might be beneficial include:

- Have you seen any strange activity in the area lately (rogue access points [APs] in wireless VoIP implementations, hackers roaming around)?
- Did the problem begin only recently, or has it been happening for some length of time?
- Are you aware of any others experiencing similar difficulties?
- When was the last time it worked?
- Is the device turned on? (Seriously?)

This last question is probably the most commonly asked question in the history of technical support, and it is still a very important question. With modern complex systems, it is very possible that the user has powered on one component of the system and not another component. Sometimes you can save the user from embarrassment by asking him or her to power cycle everything. That way, if the user did not have the hardware powered on, he or she will not have to admit it. The big key is to always handle users tactfully because you will definitely find it easier to work with users who enjoy being around you.

If you are using the newer operating systems and a software-based IP phone, you may be able to take advantage of new features that allow you to get the needed information without relying on the user. For example, in Windows Vista and Windows 7, the Reliability Monitor is an exceptional tool for viewing the historical problems and changes on a computer. To access the Reliability Monitor, press the Windows key on the keyboard (or click the Start button), type Reliability Monitor, and then press ENTER (or click the View Reliability History link that is displayed).

You will see a screen similar to the one in Figure 17-1. Notice that the Reliability Monitor shows the application failures as well as software and driver installations and removals.

**Figure 17-1** The Windows 7 Reliability Monitor

![](img/ee67e6cd30f16bc39d653f87870eabb5_480_0.png)

Now that the Research and Engage phases are complete, it’s time to move on to the Adjust phase if the problem is still unresolved. If the problem is solved, you can skip ahead to the Configure and Take Note phases or document the problem and solution, or simply close the trouble ticket if the problem is a common recurring issue.

## Adjust

Interestingly, we’ve just now arrived where I see many techs, VoIP administrators, or network administrators in general, beginning. Don’t feel bad—I’ve done it many times myself. Through years of experience, I’ve found that I can save hours of difficulty by moving through the Research and Engage phases before the Adjust phase. Keep in mind that I’m going to spend 10 to 15 minutes in most situations in these first two phases. I find that I’m more frequently finished with the first two phases in five or ten minutes. At one point, I tracked the results of using this methodology with all of my troubleshooting cases for six months. During this time I had to troubleshoot 206 unique problems (I dealt with hundreds of common problems during the same period). With 117 of the problems, I found the solution in the first two phases. This result meant that I solved more than half of the problems in less than 10 to 20 minutes.

With the remaining 89 problems, I moved on to the Adjust phase. This is the phase where you begin trying different things to see if you can track down the source of your problem. You might try updating the firmware on a wireless VoIP phone or AP. You may try installing new device drivers for a client adapter in order to make them more compatible with the VoIP software you are using. You could also change settings or disable features to see if the problem goes away. The point is that this is where you begin the “technical” side of troubleshooting. While many techs begin here, you will have an advantage because you are starting this phase with a more accurate view of the problem.

Once you've completed these first three stages, you'll have come to a solution. Again, that solution is sometimes reinstalling the application, reinstalling the operating system, or reloading factory defaults and starting over with the configuration of a router, but things are working again. You may have your solution after the Research phase, or you may have it after the Engage phase. Whether you make it all the way to the Adjust phase, or you solve the problem earlier in the process, you are now ready to move to what I call the ongoing stability phases: Configure and Take Note.

## Configure

This is the first of the two ongoing stability phases. In the Configure phase, you ensure that the systems and devices are configured and are operating according to your standards before leaving the physical area (or remote management tool). This allows you to maintain a standardized environment, and a standardized environment is usually more stable. Of course, with a reinstallation, you will need to reinstall according to the original specifications for the installation and then apply any configuration changes that have been approved or processed since that time. The primary goal of this phase is to provide consistency in your environment and to improve troubleshooting processes moving forward.

In a consistent environment, you can assume certain things. For example, you can assume that a device has the newest firmware, or you can assume that an operating system has a particular service pack loaded. The real world, however, introduces great difficulty in the area of consistency. For an environment to be and remain consistent, the following things must all be true:

- The users must be unable to make configuration changes that affect the consistency of the configurations.
- All administrators who have the power to make configuration changes must be consistent in the changes they make.
- Some automated system must be in place that adjusts the configurations of all machines or devices simultaneously.

As you can see from these three requirements, it is very difficult to have a truly consistent environment because of the human factor. However, even an environment that is mostly consistent makes troubleshooting much easier because the likelihood of an administrator implementing a bad configuration is lower than that of a user or customer. This ratio is not based on some superior intellect of the administrator; it is simply based on the training and area of specialty of the administrator. In the end, configuring your machines and devices to a standard specification generally reduces support costs by reducing support incidents.
