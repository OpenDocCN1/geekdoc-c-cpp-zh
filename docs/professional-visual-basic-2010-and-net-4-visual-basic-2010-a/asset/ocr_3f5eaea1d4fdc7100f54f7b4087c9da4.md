You still haven’t written any actual code, so this is a great time to test your application. Use F5 to build and run it. Once the build is complete, Outlook will automatically open. You should see something similar to what is shown in Figure 25-33.

![](bbox=[0.145, 0.151, 0.802, 0.545])

# FIGURE 25-33

Note that even the original Outlook test message, which was received two days previously, now includes your custom OFR. In fact, you’ll find that every message you open includes the OFR — which could easily become annoying, given that in a real application your OFR would probably be targeting a single message type. Similarly, if you choose to create a new message, there it is again — an OFR that has only display information. Once you have satisfied yourself with the impact of this region on Outlook, close Outlook and return to Visual Studio.

Figure 25-34 provides a view of the default generated code for your OFR. Your goal is to carry out two tasks: First, make this OFR display only if the associated message includes one or more attachments. Second, update Label1 so that the number of attachments is shown in the OFR.

The first item to note is the Form Region Factory code block, which has been collapsed. There are actually three generated methods, and it is the method hidden inside this code block where you’ll want to put the custom logic specifying when this OFR should be visible. When expanded, as shown in the following code, not only do you have your AdjoiningOFR class, but within this collapsed block is a second partial class definition that defines an implementation to create your OFR as part of a factory. Factories are a well-known software pattern wherein the calling application might not know the details of which class is being created, but only the base-class OFR and the methods and properties exposed at the base-class level.