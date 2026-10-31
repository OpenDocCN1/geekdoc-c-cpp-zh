to process the response. There are three design patterns that can be used for maintaining this context:

+   - Concept Maintains Asynchronous Context
+   - State Machine Maintains Asynchronous Context
+   - Process Maintains Asynchronous Context

# Concept Maintains Asynchronous Context

With this approach an inference agent sends the Request in the action part of a rule or in a preprocessor function (Figure 12-6). A concept is also created or updated with any contextual information needed to process the reply.

When the Reply is returned, the preprocessor function for the reply event retrieves the concept from the cache (assuming cache-only mode was used). To make retrieval possible, the identifier for the concept (typically the extID) must be included in the request and returned in the reply. The service provider must also be designed to return the identifier from the request in the reply. If JMS is used for the transport and the extID of the concept is used as the JMSCorrelationID of the request, the JMS specification requires that the service provider pass this same value back as the JMSCorrelationID of the reply. The reply is then processed either in the preprocessor function or in rules triggered by the arrival of the reply event.

![](bbox=[0.28, 0.8, 0.78, 0.92])

Figure 12-6: Concept Maintains Asynchronous Context