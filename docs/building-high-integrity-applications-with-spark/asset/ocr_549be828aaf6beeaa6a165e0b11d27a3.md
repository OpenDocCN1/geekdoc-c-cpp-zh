![](bbox=[0.15, 0.13, 0.85, 0.54])

Figure 8.4. Architecture of the SPARK components of Thumper.

non-SPARK sections. In the case of Thumper we identify our verification goals as ensuring freedom from runtime error when processing client input along with ensuring that an invalid or inappropriate time stamp is never returned to the client.

From a security point of view, the critical path through Thumper is that traversed by the messages received from the client on their way to becoming responses sent back to the client. We assume input messages may be malicious and purposely malformed with the intent of crashing the server or coaxing the server to generate an invalid time stamp. In contrast, Thumper's initialization and secondary logging feature are not critical because they do not depend on client input and can thus be reasonably written in full Ada.

Figure 8.4 shows the architecture of the SPARK components of Thumper. The boundary between the SPARK and non-SPARK code is marked by several boundary variable packages that encapsulate the connection to the non-SPARK components. The packages Network.Socket.Reader and Network.Socket.Writer wrap the compiler vendor's network library and provide simplified interfaces. They also hide the underlying network library to prevent vendor specific names from leaking into the rest of the program. A future version of Thumper may use a different networking library or even a different transport mechanism for messages; the SPARK components do not need to know about such changes.

For pragmatic reasons we choose to use the OpenSSL library for Thumper's cryptographic needs. This is not ideal and is particularly worrisome in light of OpenSSL's history of security problems (OpenSSL Project, 2014b). Unfortunately, at the time of this writing no open source cryptographic library supporting digital signature algorithms and written in verified SPARK is available