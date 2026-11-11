# CHAPTER 10

# # Security

# In this chapter

+   - 10.1 Class Loaders, page 530
+   - 10.2 Security Managers and Permissions, page 546
+   - 10.3 User Authentication, page 566
+   - 10.4 Digital Signatures, page 582
+   - 10.5 Encryption, page 599

When Java technology first appeared on the scene, the excitement was not about a well-crafted programming language but about the possibility of safely executing applets delivered over the Internet. Obviously, serving executable applets is only practical when the recipients can be sure the code won't wreak havoc on their machines. Security therefore was and is a major concern of both the designers and the users of Java technology. This means that unlike other languages and systems, where security was implemented as an after-thought or as a reaction to break-ins, security mechanisms are an integral part of Java technology.

Three mechanisms help ensure safety:

+   - Language design features (bounds checking on arrays, no unchecked type conversions, no pointer arithmetic, and so on).
+   - An access control mechanism that controls what the code can do (file access, network access, and so on).