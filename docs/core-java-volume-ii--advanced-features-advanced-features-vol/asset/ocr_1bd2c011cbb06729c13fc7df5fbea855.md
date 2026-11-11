# ### 10.4.6 Certificate Requests

In the preceding section, we simulated a CA with a keystore and the certificateSigner tool. However, most CAs run more sophisticated software to manage certificates, and they use slightly different formats for certificates. This section shows the added steps required to interact with those software packages.

We will use the OpenSSL software package as an example. The software is preinstalled on many Linux systems and Mac OS X, and a Cygwin port for Windows is also available. You can download the software at www.openssl.org. To create a CA, run the ca script. The exact location depends on your operating system. On Ubuntu, run

```
```
/usr/lib/ssl/misc/CA.pl -newca
```
```

This script creates a subdirectory called demoCA in the current directory. The directory contains a root key pair and storage for certificates and certificate revocation lists.

You will want to import the public key into the Java keystores of all employees, but it is in the Privacy Enhanced Mail (PEM) format, not the DER format that the keystore accepts easily. Copy the file demoCA/cacert.pem to a file acmeroot.pem and open that file in a text editor. Remove everything before the line

```
```
-----BEGIN CERTIFICATE-----
```
```

and after the line

```
```
-----END CERTIFICATE-----
```
```

Now you can import acmeroot.pem into each keystore in the usual way:

```
```
keytool -importcert -keystore cindy.certs -alias alice -file acmeroot.pem
```
```

It seems quite incredible that the keytool cannot carry out this editing operation itself.

To sign Alice's public key, start by generating a certificate request that contains the certificate in the PEM format:

```
```
keytool -certreq -keystore alice.store -alias alice -file alice.pem
```
```

To sign the certificate, run

```
```
openssl ca -in alice.pem -out alice_signedby_acmeroot.pem
```
```

As before, cut out everything outside the BEGIN CERTIFICATE/END CERTIFICATE markers from alice_signedby_acmeroot.pem. Then import it into the keystore: