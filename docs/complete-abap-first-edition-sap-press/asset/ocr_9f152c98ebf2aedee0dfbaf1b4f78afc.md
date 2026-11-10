outbound processing, and if you're creating a basic type to pass purchase order data to the external system, then the basic type should be linked to the ORDERS logical message type.

You can link the basic type to an existing logical message type or create a new logical message type if none of the existing message types describe your business process adequately. One basic type can be assigned to several logical message types and vice versa, so you should create a new message type only if none of the existing message types adequately describe your business process.

The logical message types are defined using Transaction WE81, whereas the basic type is linked to the message type using Transaction WE82.

Now that you have a better idea of the structure, types, and tools of IDocs, in the following subsections we'll walk you through IDoc development and the required configuration steps.

# Creating a Segment

Use Transaction WE31 to create a segment. The segment is added to the basic type to define the structure of the IDoc.

Proceed as follows to create a segment:

+   1. On the initial screen of Transaction WE31 (see Figure 19.34), provide the name of the segment and click the CREATE button in the application toolbar. SAP segment names start with /1, and customer segment names start with /Z.

![](bbox=[0.15, 0.65, 0.65, 0.785])

Figure 19.34 Create Development Segment Initial Screen

+   2. On the CREATE SEGMENT DEFINITION screen, as shown in Figure 19.35, maintain the fields for the segment just like you would maintain the components of a