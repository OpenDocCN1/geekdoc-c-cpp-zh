# Chapter 138:
System.DirectoryServices.Protocols.LdapConnection

# Section 138.1: Authenticated SSL LDAP connection, SSL cert does not match reverse DNS

Set up some constants for the server and authentication information. Assuming LDAPv3, but it's easy enough to change that.

```
// Authentication, and the name of the server.
private const string LDAPUser = "cn=example:app:mygroup:accts,ou=Applications,dc=example,dc=com";
private readonly char[] password = { 'p', 'a', 's', 's', 'w', 'o', 'r', 'd' };
private const string TargetServer = "ldap.example.com";

// Specific to your company. Might start "cn=manager" instead of "ou=people", for example.
private const string CompanyDN = "ou=people,dc=example,dc=com";
```

Actually create the connection with three parts: an LdapDirectoryIdentifier (the server), and NetworkCredentials.

```
// Configure server and port. LDAP w/ SSL, aka LDAPS, uses port 636.
// If you don't have SSL, don't give it the SSL port.
LdapDirectoryIdentifier identifier = new LdapDirectoryIdentifier(TargetServer, 636);

// Configure network credentials (userid and password)
var secureString = new SecureString();
foreach (var character in password)
{
    secureString.AppendChar(character);
}
NetworkCredential creds = new NetworkCredential(LDAPUser, secureString);

// Actually create the connection
LdapConnection connection = new LdapConnection(identifier, creds)
{
    AuthType = AuthType.Basic,
    SessionOptions =
    {
        ProtocolVersion = 3,
        SecureSocketLayer = true
    };
};

// Override SChannel reverse DNS lookup.
// This gets us past the "The LDAP server is unavailable." exception
// Could be
// connection.SessionOptions.VerifyServerCertificate += { return true; };
// but some certificate validation is probably good.
connection.SessionOptions.VerifyServerCertificate +=
(sender, certificate) => certificate.Subject.Contains(string.Format("CN={0},", TargetServer));
```

Use the LDAP server, e.g. search for someone by userid for all objectClass values. The objectClass is present to demonstrates a compound search: The ampersand is the boolean "and" operator for the two query clauses.

```
SearchRequest searchRequest = new SearchRequest(
    CompanyDN,
    string.Format("(&(objectClass=*)(uid={0}))", uid),
    SearchScope.Subtree,
```