Now that you have a better understanding of EDI and ALE technology, we'll dive into the use of IDocs in the next subsection.

# 19.3.3 Intermediate Documents

IDocs are used to exchange data via EDI or ALE. An IDoc is just a data container that holds data in a specific data format. For example, a date field may be stored in an IDoc with an MMDDYY format.

As previously mentioned, an IDoc consists of one control record, multiple data records, and multiple status records, as shown in Figure 19.29. The control record holds control information such as direction (inbound or outbound), sender and receiver information, message type, IDoc status, and so on. In Figure 19.29, you'll see the control record information displayed under the SHORT TECHNICAL INFORMATION section.

![](bbox=[0.142, 0.419, 0.851, 0.792])

**Figure 19.29** IDoc Example

The data records hold the application data. When developing an IDoc, we define segments (structures) that hold the application data. When the IDoc is generated,