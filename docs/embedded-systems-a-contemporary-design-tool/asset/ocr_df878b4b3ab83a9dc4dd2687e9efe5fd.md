the client believes the site has failed, every other site must be notified so that they will not attempt to used failed node.

When a failed site is repaired, it must be reintegrated into the system. Reintegration can be done by a handshaking procedure. Information to update routing tables also needs to be broadcast. Queued messages may then be delivered to the site.

# 16.10.3.2 Message Loss

The RPC semantics must specify what happens when a procedure call is repeated. In a distributed embedded application there is always a finite probability that an initial procedure call, a reply message, or a return value may be lost. Therefore, it must be assumed that a procedure call may be repeated.

Consider the following situation. An RPC is executed to increase the set point value on a boiler by a certain number of degrees. The call is received and executed, but the acknowledgement is lost. The sender times out on the response and resends. Now, a potentially dangerous situation exists: The set point should not be raised a second time.

The exact implementation of such semantics depends on whether or not the receiver maintains state. For the case in which the server maintains state, the client holds state information in some data structure. Subsequent client calls to the receiver build on the stored information. However, a server crash can potentially lose that information unbeknownst to the client. When the server (and client) does not retain state information, each transaction stands alone.

Observe an analogous situation with MPEG-encoded data. The high data compression and throughput speed are achieved by transmitting only the differences from a reference frame. If the reference is lost, the subsequent differences are irrelevant.

Several of the more common RPC call semantics are expressed here.

# 16.10.3.1 MAYBE CALL

As the name suggests, under the following case the execution of the call is uncertain. The request is sent and a timer is started. If the reply message is not received before the timer expires, the safe exit is taken with no retry. However, there is no way of knowing if the procedure call succeeded or if it was ever executed. The request message may have been lost or the server crashed; or the procedure may be executed and the reply message lost. Such semantics are unacceptable in an embedded application.

# 16.10.3.2 CALL AT LEAST ONCE

With such a scheme, unless the server has failed, it is known that the call has succeeded; however, what is not known is how many times. If a timely reply is not received from the server, the request message is retransmitted. Eventually, a reply is returned and received by the client, indicating that either the call succeeded or the server has failed. In the former case, the server may have received and executed the message more than once. If the server is designed to be idempotent – that is, an operation can be performed repeatedly with exactly the same effect as if it had been executed once – there is no problem and such semantics are acceptable. If all operations are idempotent, then there are no special needs for handling repeated requests.

idempotent

# 16.10.3.3 CALL AT MOST ONCE

at most once

At most once semantics requires that a request be executed either zero times or at most one time. If the transaction cannot be completed, the request is abandoned or the state of the