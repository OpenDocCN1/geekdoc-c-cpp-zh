# Yet Another Dimension

So far in this chapter, I have mostly talked about the logical structure of the Domain Model, which is just one dimension of the picture, of course. There are others. I'd also like to discuss different execution styles for a while. Let's start with the deployment environment set up for the feature list. There, I said that we are creating a rich client (WinForms) application without an Application Server. It could look similar to Figure 4-16.

# Figure 4-16. WinForms and no Application Server

![](bbox=[0.25, 0.44, 0.78, 0.62])

For the sake of the discussion here, let's increase the complexity quite a bit for a moment and add a requirement of an application server as shown in Figure 4-17.

# Figure 4-17. WinForms and Application Server

![](bbox=[0.2, 0.82, 0.88, 0.9])

The first question is on what tier(s) should the Domain Model execute? Should it only execute on the Application Server and then you give out dumb data structures, Data Transfer Objects (DTO) [Fowler PoEAA] to the Consumer tier? Or should the Domain Model only execute on the consumer side, and you fill it by asking for DTOs from the Application server? Or perhaps you want the