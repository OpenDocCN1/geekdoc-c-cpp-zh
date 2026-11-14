```
Second object to hash is 'CryptographyExample.Product'
- Product.ID = 79
- Product.Name = Fun Thing
- Product.Description = Something to keep the grandchildren quiet.
Generated hash (when Base=64 encoded for display) is:
1Eyal+AHf3e2yEB+sq5GDDuxl1oMm42oGLYlHIC78=
Comparing second object with hash of the first object:
- result is False.
```

# # Creating Custom Cryptography Providers

While the Cryptography block contains providers for a range of hashing and encryption algorithms, you may find that you have specific requirements that none of these algorithms can satisfy. For example, you may wish to perform some company-specific encryption technique, or implement a non-standard hashing algorithm. You may even want to apply multiple levels of encryption based on business requirements or data handling standards relevant to your industry.

> > Be aware that you may introduce vulnerabilities into your application by using non-standard or custom encryption algorithms. The strength of any algorithm you use must be verified as being suitable for your requirements, and rechecked regularly to ensure that new decryption techniques or known vulnerabilities do not compromise your application.

You can implement a custom hashing provider or a custom encryption provider, and integrate them with Enterprise Library. The Cryptography block contains two interfaces, IHashProvider and ISymmetricCryptoProvider, that define hashing and encryption provider requirements. For a custom hashing provider, you must implement the Create Hash and CompareHash methods based on the hashing algorithm you choose. For a custom encryption provider, you must implement the Encrypt and Decrypt methods based on the encryption algorithm you choose.

One other way that you may want to modify the block is to change the way that it creates and stores keys. By default, it stores keys that you provide or generate for the providers in DPAPI-encrypted disk files. You can modify the KeyManager class in the block to change this behavior, and modify the Wizard that helps you to specify the key in the configuration tools.

For more information about extending and modifying the Cryptography block, see the online documentation and the help files installed with Enterprise Library.