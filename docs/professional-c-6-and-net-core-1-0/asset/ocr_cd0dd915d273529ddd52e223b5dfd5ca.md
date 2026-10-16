> NOTE This program runs on your system only if the Windows groups Sales and Developers are defined. You can change the program to use groups that are available in your environment.

```
private void WriteAcl(string filename)
{
    var salesIdentity = new NTAccount("Sales");
    var developersIdentity = new NTAccount("Developers");
    var everyOneIdentity = new NTAccount("Everyone");

    var salesAce = new FileSystemAccessRule(salesIdentity,
        FileSystemRights.Write, AccessControlType.Deny);
    var everyoneAce = new FileSystemAccessRule(everyOneIdentity,
        FileSystemRights.Read, AccessControlType.Allow);
    var developersAce = new
FileSystemAccessRule(developersIdentity,
        FileSystemRights.FullControl, AccessControlType.Allow);

    var securityDescriptor = new FileSecurity();
    securityDescriptor.SetAccessRule(everyoneAce);
    securityDescriptor.SetAccessRule(developersAce);
    securityDescriptor.SetAccessRule(salesAce);

    File.SetAccessControl(filename, securityDescriptor);
}
```

> NOTE You can verify the access rules by opening the Properties window and selecting a file in Windows Explorer. Select the Security tab to see the ACL.

# Distributing Code Using Certificates

You can make use of digital certificates and sign assemblies so that consumers of the software can verify the identity of the software publisher. Depending on where the application is used, certificates may be required. For example, with ClickOnce, the user installing the application can verify the certificate to trust the publisher. Using Windows Error Reporting, Microsoft uses the certificate to determine which vendor to map to the error report.

> NOTE ClickOnce is explained in Chapter 36,"Deploying Windows Apps."

In a commercial environment, you obtain a certificate from a company such as Verisign or Thawte. The advantage of buying a certificate from a supplier instead of creating your own is that it provides a high level of trust in the authenticity of the certificate; the supplier acts as a trusted third party. For test purposes, however, .NET includes a command-line utility you can use to create a test certificate. The process of creating certificates and using them for publishing software is complex, but this