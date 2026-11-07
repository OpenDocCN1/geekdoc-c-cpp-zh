```
// Create a new NETCONF message

xmlDocPtr doc = xmlNewDoc(BAD_CAST "1.0");

xmlNodePtr rpc = xmlNewNode(NULL, BAD_CAST "rpc");

xmlNewProp(rpc, BAD_CAST "message-id", BAD_CAST
"101");

xmlDocSetRootElement(doc, rpc);

// Add an operation to the message

xmlNewChild(rpc, NULL, BAD_CAST "get-config", NULL);

// Send the message over SSH using libssh

ssh_session session;

// Setup SSH session here

ssh_channel channel = ssh_channel_new(session);

// Send the XML document as a string over the channel
```