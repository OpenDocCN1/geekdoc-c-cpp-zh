It must be secure to protect against brute force attacks, and it must be responsive to service authentication requests in a timely fashion. Certificates are usually stored in a centralized certificate store (known as a certificate server or certificate authority) as well as on the client using the certificate for authentication. Both locations must be secure, or the benefit of using certificates is diminished. In addition to the standard certificate store, users may choose to back up their certificates to disk. These backups are usually password protected, but brute force attacks against the media store may reveal the certificate given enough time. For this reason, users should be well-educated in this area and understand the vulnerability presented by the existence of such backups.

Access methods vary by authentication system and storage method, but there are standards that define credential access methods. One example is LDAP (Lightweight Directory Access Protocol). LDAP is a standard method for accessing directory service information. This information can include many objects, but is usually inclusive of authentication credentials. LDAP is, or can be, used by Lotus Notes, Novell’s Directory Services, and Microsoft’s Active Directory among others.

Sometimes, one type of authentication is not sufficient. In these cases, multi-factor authentication can be used. Multi-factor authentication is a form of authentication that uses more than one set of credentials. An example of a multi-factor authentication process would be the use of both passwords and thumb scanners. Usually, the user would place both the thumb on the thumb scanner and then be prompted for a password or PIN (personal identification number) code. The password may be used for network authentication, or it may only be used for localized authentication before the thumb data is used for network authentication. However, in most cases the password and thumb data are used to authenticate to the local machine and then to the network or just to the network alone. A common example of multi-factor authentication would be your ATM card. You have the card and you know the PIN (something you have and something you know).

There are many common credential types. They include:

+   - Username and password
+   - Certificates
+   - PACs (Privilege Attribute Certificates)
+   - Biometrics
+   - Tokens

Username and password pairs are the most popular type of credential. They are used by most network operating systems including Novell NetWare, Linux, Unix, and Windows. Due to the human factor involved in the selection of the password,