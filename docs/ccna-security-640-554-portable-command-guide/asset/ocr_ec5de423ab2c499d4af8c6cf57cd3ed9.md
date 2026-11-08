| Attack | Details |
|---|---|
| **Chosen-ciphertext attack** | ▪ Attacker chooses the ciphertext and observes the cleartext output.<br>▪ This attack might not be very practical because it is often difficult or impossible to capture both the ciphertext and plaintext. |
| **Man-in-the-middle attack** | ▪ Attacker knows a portion of the plaintext and the corresponding ciphertext.<br>▪ The plaintext is encrypted with every possible key, and the results are stored.<br>▪ The ciphertext is then decrypted by using every key until one of the results matches one of the stored values. |

# ## Cryptographic Processes in VPNs

Cryptography provides key services to VPN technologies and solutions:

| Service | Description |
|---|---|
| **Confidentiality** | The assurance that no one can read a particular piece of data except the receiver explicitly intended |
| **Integrity** | The assurance that data has not been altered in transit, intentionally or unintentionally |
| **Authentication** | The assurance the other entity is who he, she, or it claims to be |
| **Key management** | The generation, exchange, storage, safeguarding, use, vetting, and replacement of keys |

VPN services use a combination of cryptographic technologies and algorithms to accomplish their goals. For example, in site-to-site VPNs, IP packets use the following:

+   - Symmetric encryption algorithms to encrypt the payload, with keys negotiated by key management protocols
+   - Asymmetric encryption algorithms to create digital signatures and authenticate the VPN peers
+   - Hashing functions to provide checksum-type integrity checks

**NOTE:** This combination of algorithms and cryptographic methods negotiates the security settings to accomplish confidentiality, integrity, and authentication.