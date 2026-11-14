In this chapter, we will continue to refine that model by subclassing it into two more specific models, one focusing on local devices and the other on remote devices. Each will then be studied in two steps. First, the model is introduced and its unique characteristics are examined. Next, a detailed discussion illustrates how it applies, in general, to real-world situations. The following two chapters will illustrate the application of each to specific real-world situations.

In the model, local devices are assumed to be in close proximity to the core system, while remote devices are often at much greater distances and tend to be network based. The model does not distinguish between macro peripheral devices that are implemented as independent standalone units and micro devices that may be implemented within a single system or network on a chip. We will begin with the local device model followed by a similar study of the remote model.

# 16.2 THE LOCAL DEVICE MODEL

A high-level architecture of the local device model utilizing a local external bus is given in Figure 16.2. In the model, the information, the source and destination, and the control and synchronization over the local bus structure are supported through the following sets of signals:

+   • Address
+   • Data
+   • Control.

![](bbox=[0.283, 0.475, 0.82, 0.77])

Figure 16.2 The Local Device Model Architecture

address, places,
information data,
control

The address information provides the means of identifying the places where the information or data is to be written or read from in the model. The control signals implement the control and synchronization that is unique to the local device model and provide the physical means by which a transaction is directed and coordinated. Each of these can be implemented in a variety of ways depending on the nature and structure of the underlying