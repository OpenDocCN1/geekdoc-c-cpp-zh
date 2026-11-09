how users can interact with your system and ensure that your system carefully protects its data. always verifying that the user is allowed to perform a given action by the security policy. You need to be paranoid in doing this: make your application check and recheck the credentials/authentication of its users.

And you need to design your system with the idea that it will come under attack. You need to be aware of the different kinds of attacks that can be made against it, implement safeguards against those attacks, monitor your application to detect active attacks like DoS, and respond with the tools at your disposal when an attack is detected.

# ## References and Resources

+   - **CIDR Notation** ............................ [http://en.wikipedia.org/wiki/CIDR_notation](http://en.wikipedia.org/wiki/CIDR_notation)
+     A Wikipedia article on the standard IP address notation used for managing IP address blocks, as used by App Engine’s Denial-of-Service protection system.

+   - **OpenSSL** .................................. [http://www.openssl.org/](http://www.openssl.org/)
+     A standard, widely used implementation of the secure sockets layer. The site includes both a fantastic implementation and extensive documentation on the library, the underlying SSL protocol, and how to use it correctly.

+   - **Common Gateway Interface (CGI)** .................... [http://www.w3.org/CGI/](http://www.w3.org/CGI/)
+     The official standard and documentation for CGI.

+   - **Understanding Denial-of-Service Attacks. . .**
+     . . . [http://www.us-cert.gov/cas/tips/ST04-015.html](http://www.us-cert.gov/cas/tips/ST04-015.html)
+     An excellent article from the US Computer Emergency Readiness Team explaining the mechanics of denial-of-service attacks and how to recognize, protect against, and respond to them.