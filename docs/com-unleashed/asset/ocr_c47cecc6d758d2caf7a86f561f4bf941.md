Library. The MSMQ ActiveX queue objects maintain a single cursor behind the scenes. Both mechanisms enable messages to be examined and optionally removed as cursors are advanced through the queue. Because several applications can interact with a queue concurrently, cursors might not always point to a message. Such is the case when another application removes a message from a queue after your application has already advanced its cursor to that message, but before your application has a chance to actually remove the message.

Cursors are used only when you are interested in messages that are not at the front of the queue. Although most queue processing will probably operate in the established FIFO manner, some out-of-band operations might be necessary—for example, displaying the labels of all the pending messages in a particular queue for administrative purposes.

# ## MSMQ API Cursors

The MSMQ Library API treats cursors as separate objects that must be created and released much like any other resource. This enables an application to create several cursors to track multiple locations in the same queue. The following API routines create and release cursor resources:

+   - MQCreateCursor()
+   - MQCloseCursor()

The MQReceiveMessage() routine, as you might have noticed, is one of the most complex functions in the MSMQ Library. Previously, you only worked with the timeout feature to acquire nonblocking synchronous behavior. You'll be learning many new uses for the MQReceiveMessage() routine in this chapter. First, be aware that MQReceiveMessage() can take an optional cursor handle, which supports three different actions:

+   - MQ_ACTION_RECEIVE
+   - MQ_ACTION_PEEK_CURRENT
+   - MQ_ACTION_PEEK_NEXT

Peek operations retrieve message data but, unlike the receive action, do not remove the message from the queue. If a NULL cursor handle is supplied to MQReceiveMessage(), only the message at the front of the queue can be operated on. The peek-next action requires a cursor, which is moved to a next location before the message is peeked. Receiving a message will automatically update the cursor to the next message in the queue. It is important to execute the MQ_ACTION_PEEK_CURRENT to initialize a cursor before attempting to use MQ_ACTION_PEEK_NEXT.