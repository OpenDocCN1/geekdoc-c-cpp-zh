high likelihood, be different. A cryptographic hash is similar to a checksum except that it is computationally infeasible for anyone to find a document that generates a particular hash value or modify a document in such a way as to generate the same hash value. When a high quality cryptographic hash algorithm is used, it is also computationally infeasible to find two different documents that generate the same hash value, a property sometimes called strong collision resistance.

A public/private key pair is a related pair of keys such that material encrypted by the public key can only be decrypted by the corresponding private key. Typically, a user keeps the private key secret but distributes the public key widely allowing people the user does not know to send encrypted messages that only the user can read.

A digital signature is a unit of data attached to a message obtained by processing a cryptographic hash of that message with the signer's private key. The signature can be verified by anyone using the corresponding public key. A successful verification shows both that the message was unmodified, because any modification would (with high likelihood) change the hash, and that the signer is authentic because only the owner of the private key can make a signature that is verifiable with the corresponding public key.

Here is how Alice obtains a time stamp for one of her documents using a time stamp server:

+   1. Alice computes a cryptographic hash H of her document.
+   2. Alice sends H to the server.
+   3. The server appends the current time to H and then digitally signs the combination. The result is the time stamp.
+   4. The server returns the time stamp to Alice.
+   5. Alice verifies the time stamp by checking the time it contains is reasonable, the hash it contains is still H, and the digital signature on the time stamp is valid.

Later Alice submits her document together with its time stamp to Bob. Bob computes the hash H of the document and verifies that it agrees with the hash in the time stamp. He also verifies the server's digital signature. If Bob believes the server has not been compromised and trusts the server to have an accurate time, he must agree that Alice's document existed at or before the time mentioned in the time stamp.7

Even though Alice holds the time stamp, she cannot defeat this protocol. Modifying her document after obtaining the time stamp will change its hash. If she tries to tamper with the time stamp itself to change either the hash or time stored in it, she will invalidate the server's signature. Notice that Alice does