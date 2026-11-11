
her by sending messages, such as money transfer instructions, that others will believe came from Alice.

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_611_0.png)

**Figure 10.9** Public key signature exchange with DSA

### 10.4.3 Verifying a Signature

The JDK comes with the keytool program, which is a command-line tool to generate and manage a set of certificates. We expect that ultimately the functionality of this tool will be embedded in other, more user-friendly programs. But right now, we’ll use keytool to show how Alice can sign a document and send it to Bob, and how Bob can verify that the document really was signed by Alice and not an impostor.

The keytool program manages keystores—databases of certificates and private/public key pairs. Each entry in the keystore has an alias. Here is how Alice creates a keystore alice.certs, and generates a key pair with alias alice:

```text
keytool -genkeypair -keystore alice.certs -alias alice
```

When creating or opening a keystore, you are prompted for a keystore password. For this example, just use secret. If you were to use the keytool-generated

If Bob wants to check that he got the right certificate, he can call Alice and verify the certificate fingerprint over the phone.

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_613_0.png)

> **NOTE:** Some certificate issuers publish certificate fingerprints on their web sites. For example, to check the DigiCert certificate in the keystore `jre/lib/security/cacerts` directory, use the `-list` option:

```text
keytool -list -v -keystore jre/lib/security/cacerts
```

The password for this keystore is changeit. One of the certificates in this keystore is

```text
Owner: CN=DigiCert Assured ID Root G3, OU=www.digicert.com, O=DigiCert Inc, C=US
Issuer: CN=DigiCert Assured ID Root G3, OU=www.digicert.com, O=DigiCert Inc, C=US
Serial number: ba15afa1ddfa0b54944afdc24a06cec
Valid from: Thu Aug 01 14:00:00 CEST 2013 until: Fri Jan 15 13:00:00 CET 2038
Certificate fingerprints:
         SHA1:  F5:17:A2:4F:9A:48:C6:C9:F8:A2:00:26:9F:DC:0F:48:2C:AB:30:89
         SHA256: 75:37:CB:88:4C:47:09:0C:AB:36:55:1B:A6:F4:5D:B8:40:68:0F:BA:
                 16:6A:95:2D:B1:00:71:7A:35:3F:C2
```

You can check that your certificate is valid by visiting the web site
www.digicert.com/digicert-root-certificates.htm.

Once Bob trusts the certificate, he can import it into his keystore.

```text
keytool -importcert -keystore bob.certs -alias alice -file alice.cer
```

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_613_1.png)

> **CAUTION:** Never import into a keystore a certificate that you don’t fully trust. Once a certificate is added to the keystore, any program that uses the keystore assumes that the certificate can be used to verify signatures.

Now Alice can start sending signed documents to Bob. The jarsigner tool signs and verifies JAR files. Alice simply adds the document to be signed into a JAR file.

```text
jar cvf document.jar document.txt
```

She then uses the jarsigner tool to add the signature to the file. She needs to specify the keystore, the JAR file, and the alias of the key to use.

```text
jarsigner -keystore alice.certs document.jar alice
```

When Bob receives the file, he uses the -verify option of the jarsigner program.

```text
jarsigner -verify -keystore bob.certs document.jar
```

Bob does not need to specify the key alias. The jarsigner program finds the X.500 name of the key owner in the digital signature and looks for a matching certificate in the keystore.

If the JAR file is not corrupted and the signature matches, the jarsigner program prints

```text
jar verified.
```

Otherwise, the program displays an error message.

### 10.4.4 The Authentication Problem

Suppose you get a message from your friend Alice, signed with her private key, using the method we just showed you. You might already have her public key, or you can easily get it by asking her for a copy or by getting it from her web page. Then, you can verify that the message was in fact authored by Alice and has not been tampered with. Now, suppose you get a message from a stranger who claims to represent a famous software company, urging you to run a program attached to the message. The stranger even sends you a copy of his public key so you can verify that he authored the message. You check that the signature is valid. This proves that the message was signed with the matching private key and has not been corrupted.

Be careful: *You still have no idea who wrote the message.* Anyone can generate a pair of public and private keys, sign the message with the private key, and send the signed message and the public key to you. The problem of determining the identity of the sender is called the *authentication problem.*

The usual way to solve the authentication problem is simple. Suppose the stranger and you have a common acquaintance you both trust. Suppose the stranger meets your acquaintance in person and hands over a disk with the public key. Your acquaintance later meets you, assures you that he met the stranger and that the stranger indeed works for the famous software company, and then gives you the disk (see Figure 10.10). That way, your acquaintance vouches for the authenticity of the stranger.

In fact, your acquaintance does not actually need to meet you. Instead, he can use his private key to sign the stranger’s public key file (see Figure 10.11).

When you get the public key file, you verify the signature of your friend, and because you trust him, you are confident that he did check the stranger’s credentials before applying his signature.

However, you might not have a common acquaintance. Some trust models assume that there is always a “chain of trust”—a chain of mutual acquaintances—so that you trust every member of that chain. In practice, of course,

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_616_0.png)

Figure 10.11  Authentication through a trusted intermediary’s signature

### 10.4.5 Certificate Signing

In Section 10.4.3, “Verifying a Signature,” on p. 589 you saw how Alice used a self-signed certificate to distribute a public key to Bob. However, Bob needed to ensure that the certificate was valid by verifying the fingerprint with Alice.

Suppose Alice wants to send her colleague Cindy a signed message, but Cindy doesn’t want to bother with verifying lots of signature fingerprints. Now suppose there is an entity that Cindy trusts to verify signatures. In this example, Cindy trusts the Information Resources Department at ACME Software.

That department operates a *certificate authority* (CA). Everyone at ACME has the CA’s public key in their keystore, installed by a system administrator who carefully checked the key fingerprint. The CA signs the keys of ACME employees. When they install each other’s keys, the keystore will trust them implicitly because they are signed by a trusted key.

Here is how you can simulate this process. Create a keystore `acmesoft.certs`. Generate a key pair and export the public key:

```text
keytool -genkeypair -keystore acmesoft.certs -alias acmeroot
keytool -exportcert -keystore acmesoft.certs -alias acmeroot -file acmeroot.cer
```

The public key is exported into a “self-signed” certificate. Then, add it to every employee’s keystore:

```text
keytool -importcert -keystore cindy.certs -alias acmeroot -file acmeroot.cer
```

For Alice to send messages to Cindy and to everyone else at ACME Software, she needs to bring her certificate to the Information Resources Department and have it signed. Unfortunately, this functionality is missing in the `keytool` program. In the book’s companion code, we supply a CertificateSigner class to fill the gap. An authorized staff member at ACME Software would verify Alice’s identity and generate a signed certificate as follows:

```text
java CertificateSigner -keystore acmesoft.certs -alias acmeroot \
  -infile alice.cer -outfile alice_signedby_acmeroot.cer
```

The certificate signer program must have access to the ACME Software keystore, and the staff member must know the keystore password. Clearly, this is a sensitive operation.

Alice gives the file `alice_signedby_acmeroot.cer` to Cindy and to anyone else in ACME Software. Alternatively, ACME Software can simply store the file in a company directory. Remember, this file contains Alice’s public key and an assertion by ACME Software that this key really belongs to Alice.

Now Cindy imports the signed certificate into her keystore:

```text
keytool -importcert -keystore cindy.certs -alias alice -file alice_signedby_acmeroot.cer
```

The keystore verifies that the key was signed by a trusted root key that is already present in the keystore. Cindy is *not* asked to verify the certificate fingerprint.

Once Cindy has added the root certificate and the certificates of the people who regularly send her documents, she never has to worry about the keystore again.
