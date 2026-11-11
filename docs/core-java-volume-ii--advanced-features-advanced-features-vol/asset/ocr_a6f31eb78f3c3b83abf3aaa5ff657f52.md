Bob does not need to specify the key alias. The jarsigner program finds the X.500 name of the key owner in the digital signature and looks for a matching certificate in the keystore.

If the JAR file is not corrupted and the signature matches, the jarsigner program prints

```
jar verified.
```

Otherwise, the program displays an error message.

# 10.10.4 The Authentication Problem

Suppose you get a message from your friend Alice, signed with her private key, using the method we just showed you. You might already have her public key, or you can easily get it by asking her for a copy or by getting it from her web page. Then, you can verify that the message was in fact authored by Alice and has not been tampered with. Now, suppose you get a message from a stranger who claims to represent a famous software company, urging you to run a program attached to the message. The stranger even sends you a copy of his public key so you can verify that he authored the message. You check that the signature is valid. This proves that the message was signed with the matching private key and has not been corrupted.

Be careful: *You still have no idea who wrote the message.* Anyone can generate a pair of public and private keys, sign the message with the private key, and send the signed message and the public key to you. The problem of determining the identity of the sender is called the *authentication problem.*

The usual way to solve the authentication problem is simple. Suppose the stranger and you have a common acquaintance you both trust. Suppose the stranger meets your acquaintance in person and hands over a disk with the public key. Your acquaintance later meets you, assures you that he met the stranger and that the stranger indeed works for the famous software company, and then gives you the disk (see Figure 10.10). That way, your acquaintance vouches for the authenticity of the stranger.

In fact, your acquaintance does not actually need to meet you. Instead, he can use his private key to sign the stranger’s public key file (see Figure 10.11).

When you get the public key file, you verify the signature of your friend, and because you trust him, you are confident that he did check the stranger’s credentials before applying his signature.

However, you might not have a common acquaintance. Some trust models assume that there is always a “chain of trust”—a chain of mutual acquaintances—so that you trust every member of that chain. In practice, of course,