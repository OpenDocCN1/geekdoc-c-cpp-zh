```
Variable<string> roomName = new Variable<string>();
Variable<double> width = new Variable<double>();
Variable<double> depth = new Variable<double>();

// Receive room information
Receive receiveRoomInfo = new Receive
{
 OperationName = "UploadRoomInformation",
 ServiceContractName = XName.Get("IProperty", ns),
 CorrelatesWith = operationHandle,
 CorrelatesOn = extractGuidFromUploadRoomInformation,
 Content = new ReceiveParametersContent
 {
  Parameters =
  {
   {"propertyId", new OutArgument<Guid>()},
   {"roomName", new OutArgument<string>(roomName)},
   {"width", new OutArgument<double>(width)},
   {"depth", new OutArgument<double>(depth)}
  }
 };
};
```

The variables initially defined are used to record the data passed from the client to the workflow. Again the Receive activity specifies both the OperationName and the ServiceContractName so that metadata can be generated for this operation. The CorrelatesWith value is critical here, as it links the different operations of the workflow together. In the SendReply activity, we created this handle so that we could reference it with these later operations. Without this handle, it would not be possible to work out which workflow instance an incoming message is for.

The CorrelatesOn property defines what is extracted from the incoming message in order to verify that the message is for this workflow instance. Again, a MessageQuerySet is used, which in this case extracts the unique ID from the incoming message:

```
MessageQuerySet extractGuidFromUploadRoomInformation =
 new MessageQuerySet
 {
  {"PropertyId",
   new XPathMessageQuery
   { "@sm:body()//local:UploadRoomInformation/local:propertyId",
     messageContext: }
  }
};
```

Here, the XPath is looking for the propertyId element within the UploadRoomInformation call.

The last part of this Receive defines what happens with the incoming parameters passed to the service operation. Here, I'm expecting the unique propertyId, a room name and dimensions. This data is extracted into variables, and in the example code we simply output it to the console. In a real application, you would obviously use this data to update a database or something similar.

The last Receive activity is used to await the DetailsComplete message from the client. It follows a similar pattern to the other receive activities in that it defines the service contract name and operation name, uses the same correlation handle as the initial Send and the Receive used for the UploadRoomInformation operation, and it uses a MessageQuerySet in order to retrieve the unique property ID from the incoming message.

With those activities in place, the rest of the workflow is a while loop that contains the Pick activity and its branches:

```
new While
{
 Condition = ExpressionServices.Convert<bool>
 (/env => !finished.Get(env)),
 Body = new Pick
```