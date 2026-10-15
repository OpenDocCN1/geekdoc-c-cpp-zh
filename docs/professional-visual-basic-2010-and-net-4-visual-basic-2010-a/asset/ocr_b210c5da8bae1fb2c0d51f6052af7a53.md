```
X509Certificate.CreateFromCertFile(certFilePath)
textbox.Text = "Hash = " & cert.GetCertHashString() & Environment.NewLine
textbox.Text &= "Effective Date = " & 
cert.GetEffectiveDateString() & Environment.NewLine
textbox.Text &= "Expire Date = " & 
cert.GetExpirationDateString() & Environment.NewLine
textbox.Text &= "Issued By = " & cert.Issuer & Environment.NewLine
textbox.Text &= "Issued To = " & cert.Subject & Environment.NewLine
textbox.Text &= "Algorithm = " & cert.GetKeyAlgorithm() & Environment.NewLine
textbox.Text &= "Pub Key = " & cert.GetPublicKeyString() & Environment.NewLine
End Sub
End Class
```

Code snippet from CertLoad.vb

The static method loads CreateFromCertFile (the certificate file) and creates a new instance of the class X509Certificate. When working correctly, the results are displayed in ProVB_Security as shown in Figure 32-11. The next section deals with Secure Sockets Layer (SSL), which uses X.509 certificates to establish the trust relationship.

![](bbox=[0.13, 0.34, 0.7, 0.66])

FIGURE 32-11

# Secure Sockets Layer

The Secure Sockets Layer (SSL) protocol provides privacy and reliability between two communicating applications over the Internet. SSL is built over the TCP layer. In January 1999, the Internet Engineering Task Force (IETF) adopted an enhanced version of SSL 3.0 called Transport Layer Security (TLS). TLS is backwardly compatible with SSL, and is defined in RFC 2246. However, the name SSL was retained due to wide acceptance of this Netscape protocol name. This section provides a simplified overview of the SSL algorithm sequence. SSL provides connection-oriented security via the following four properties:

+   Connection is private and encryption is valid for the current session only.
+   Symmetric key cryptography, like DES, is used for encryption. However, the session symmetric key is exchanged using public key encryption.