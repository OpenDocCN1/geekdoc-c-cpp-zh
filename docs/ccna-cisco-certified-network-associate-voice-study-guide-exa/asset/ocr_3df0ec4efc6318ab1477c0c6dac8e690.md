+   7. ☑ **B is correct.** SIP headers use simple ASCII text-based encoding. The headers consist of field/value pairs.
+   
+   ☒ **A, C, and D are incorrect.** Neither binary nor HEX encoding is used for SIP headers. The ASCII encoding is used and maintains a simple header format much like SMTP. AES is an encryption algorithm, and the headers are not formatted according to an encryption algorithm.

# 640-460: Describe SIP Signaling Protocols

+   8. ☑ **A is correct.** While the OSI model does include a Session layer (Layer 6 of the OSI model), the SIP architecture includes only the four layers named syntax and encoding, transport, transaction, and transaction user layers.
+   
+   ☒ **B, C, and D are incorrect.** The syntax and encoding layer is responsible for the format of the SIP messages. The transaction layer manages the transactions that take place within SIP communications. The transport layer is responsible for getting the messages to the appropriate UA.

+   9. ☑ **C is correct.** The transport layer would be responsible for getting the SIP requests to the SIP server (UAS) because it is responsible for delivery of all SIP messages (both requests and responses).
+   
+   ☒ **A, B, and D are incorrect.** The transaction layer ensures that the transactions are managed properly in SIP communications. The transaction user is the logical entity utilizing the SIP protocol. The Session layer is an OSI model layer and not a SIP layer.

+   10. ☑ **A, B, and C are correct.** The FROM field is required, and it indicates the sender of the SIP message. The To field is required, and it indicates the target of the SIP message. The MAX-FORWARDS field is required, and it indicates the maximum number of allowed hops in the route to the recipient of the SIP message.
+   
+   ☒ **D is incorrect.** The CONTACT header field is an optional header field in SIP messages.

+   11. ☑ **B is correct.** The INVITE method is used to initiate a SIP call.
+   
+   ☒ **A, C, and D are incorrect.** No such method as the INVOKE method exists. The REGISTER method is used to register with the SIP registrar server. The INFO method is used to perform signaling within a live SIP call session.

+   12. ☑ **B is correct.** The messages from 200 to 299 (2xx) are reserved for successful responses. For example, response code 200 means OK.
+   
+   ☒ **A, C, and D are incorrect.** The 1xx response codes are informational. The 3xx response codes are used for redirection responses. The 4xx response codes are failure responses.