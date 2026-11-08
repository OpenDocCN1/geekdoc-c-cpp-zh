# # SELF TEST ANSWERS

**642–436: Describe sRTP**

+   1. ☑ **C is correct.** RFC 3711 defines both sRTP and sRTCP. The RFC specifies the encryption solutions and the authentication process. It details the header format for sRTP and sRTCP packets. RFC 3711 is a profile for RTP.
+   
+      ☒ **A, B, and D are incorrect.** RFC 3551 defines the audio/video profiles for RTP. RFC 3750 defines transition scenarios for moving to IPv6. RFC 3550 defines RTP and RTCP, but not the security profile, which is defined in RFC 3711.

+   2. ☑ **A, B, and C are correct.** sRTP provides confidentiality (encryption) and authentication of the RTP headers and encrypted payload. Integrity is also provided because the sequence numbers in the RTP header are authenticated.
+   
+      ☒ **D is incorrect.** Permissions are not part of sRTP. In fact, sRTP does not provide authorization functions. Authorization should be managed at the point of network ingress.

+   3. ☑ **B is correct.** The master key allows for a single key to be used in the generation of unique session keys within an RTP stream.
+   
+      ☒ **A, C, and D are incorrect.** No such keys as the primary key, subordinate key, or peer key are used in sRTP communications.

+   4. ☑ **B is correct.** Session keys are used to perform the actual encryption of the RTP payload. The master key is used to derive the session keys.
+   
+      ☒ **A, C, and D are incorrect.** The master key is utilized in the session key derivation process, but it is not used for the encryption of the RTP payload. The master key identifier (MKI) is a field in the sRTP header used to identify which master key was used to derive the session key. The authentication tag includes authentication information to authenticate the RTP header and encrypted payload.

+   5. ☑ **C is correct.** Key salting is a technique used to prevent pre-computational cracking. Pre-computational cracking attempts use previously generated dictionaries for cracking. The salting modifies the key enough so that it will not match the pre-computed tables.
+   
+      ☒ **A, B, and D are incorrect.** Master keys provide for simple generation of session keys, but they do not help prevent pre-computational attacks. Session keys are used to encrypt data, but in order for them to be secured against pre-computational attacks, they are often used with key salting. Key peppering is not a term used in encryption processing.