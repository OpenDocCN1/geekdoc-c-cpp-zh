# Working Outside of the Processor I: Refining the Model of Interprocess Communication

# THINGS TO LOOK FOR ...

+   - Critical components of the shared variable interpretation of the communication model.
+   - Critical components of the message-based interpretation of the communication model.
+   - Various ways of implementing the shared variable and message-based interpretations of the model.

# 16.1 COMMUNICATION AND SYNCHRONIZATION WITH THE OUTSIDE WORLD

In the previous chapter, we established the foundation for how an embedded application can interact with the external world. We began by extending the internal interprocess and communication model developed in Chapter 4 by incorporating a transport component. That model is repeated here in Figure 16.1.

![](bbox=[0.27, 0.57, 0.63, 0.81])

Figure 16.1 The Interprocess Communication Model