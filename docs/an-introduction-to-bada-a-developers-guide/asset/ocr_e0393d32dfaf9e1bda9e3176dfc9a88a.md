This namespace contains classes and methods to support various types of encryption and decryption. There are four basic types of encryption supported: one-way encryption using hashing, encryption using a secret key, encryption using a public and private key, and the use of digital signatures.

Public/private key pairs are used in two ways: to encrypt a message with a public key so that only the person with the corresponding private key can read it and to use a private key to digitally sign a document. Anyone with the public key can read the message, but signing it with a digital signature provides proof that it has not been tampered with.

The RsaCipher and RsaSignature classes provide support for encrypting and signing with public/private key pairs.

```
Osp::Social
```

# Declared In:

FSocial.h

# Library:

FSocial, FSocialLifelog (if you are accessing the lifelog)

# Privileges Required:

Using the features of this namespace will require at least one of the privileges listed in the table below, depending on what functionality you implement:

| Privilege group | Privilege level | Description |
| ADDRESSBOOK | NORMAL | Accessing the address book on the device |
| CALENDARBOOK | NORMAL | Accessing the calendar on the device |
| LIFELOG | SYSTEM | Accessing the lifelog |

# Summary

Selected important classes:

+   - Addressbook
+   - Calendarbook
+   - Lifelog

The Social namespace contains classes to maintain the user’s personal data, address book, calendar, and lifelog on a device. The lifelog is a log of activities over a certain period of time, including calling and messaging, together with cell-based location information. You can think of this namespace