# Hashing

The most common security function that you will perform is hashing. Consider the situation where you need to build a function to authenticate users before they can use your application. You would require the user to supply a set of login credentials, generally containing a user name and a password. This login information needs to be persisted to a database. Quite commonly, developers store the passwords of users verbatim on a database. That's a big security risk because hackers who get a chance to glance at the users' database would be able to obtain the passwords of your users. A better approach is to store the hash values of the users' passwords instead of the passwords themselves. A hashing algorithm has the following properties:

+   - It maps a string of arbitrary length to small binary values of a fixed length, known as a hash value.
+   - The hash value of a string is unique, and small changes in the original string will produce a different hash value.
+   - It is improbable that you'd find two different strings that produce the same hash value.
+   - It is impossible to use the hash value to find the original string.

Then, when the user logs in to your application, the hash value of the password provided is compared with the hash value stored in the database. In this way, even if hackers actually steal the users' database, the actual password is not exposed. One downside to storing the hash values of users' passwords is that in the event that a user loses her password, there is no way to retrieve it. You'd need to generate a new password for the user and request that she change it immediately. But this inconvenience is a small price to pay for the security of your application.

There are many hashing algorithms available in .NET, but the most commonly used are the SHA1 and MD5 implementations. Let's take a look at how they work in .NET.

Using Visual Studio 2008, create a new Console application project. Import the following namespaces:

```
using System.IO;
using System.Security.Cryptography;
```

Define the following function:

```
static void Hashing_SHA1()
{
    //---ask the user to enter a password---
    Console.Write("Please enter a password: ");
    string password = Console.ReadLine();

    //---hash the password---
    byte[] data = ASCIIEncoding.ASCII.GetBytes(password);
    byte[] passwordHash;
    SHA1CryptoServiceProvider sha = new SHA1CryptoServiceProvider();
    passwordHash = sha.ComputeHash(data);

    //---ask the user to enter the same password again---
    Console.Write("Please enter password again: ");
    password = Console.ReadLine();
```