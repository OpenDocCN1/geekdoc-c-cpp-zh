generate a key for the algorithm. Other providers, such as SHA and MD5, do not require a key. As a general recommendation, you should aim to use at minimum the SHA256 algorithm for hashing, and preferably a more robust version such as SHA384 or SHA512.

You can use two different types of **Symmetric Encryption Provider** in the Cryptography block (in addition to custom providers that you create). You can choose the DPAPI provider, or one of the well-known symmetric algorithms such as AES or 3DES. As a general recommendation, you should aim to use the AES (Rijndael) algorithm for encryption.

> Comprehensive information about the many different encryption and hashing algorithms is contained in the Handbook of Applied Cryptography (Menezes, Alfred J., Paul C. van Oorschot and Scott A. Vanstone, CRC Press, October 1996, ISBN: 0-8493-8523-7). See http://www.cacr.math.uwaterloo.ca/hac/ for more information. You will also find a list of publications that focus on cryptography at "Additional Documentation on Cryptography" (http://msdn.microsoft.com/en-us/library/aa375543(VS.85).aspx).

# CONFIGURING CRYPTOGRAPHIC PROVIDERS

In addition to the obvious properties for each cryptographic provider you add to your configuration, such as the name, some providers require you to specify an encryption key. If you already have a DPAPI-encrypted key file for the selected algorithm type, you can use this. Alternatively, you can copy an existing plain text value of the appropriate size and use this as the key value. The third approach is to allow the Enterprise Library configuration to generate a new key for you.

When you add a provider that requires a key to your configuration, the configuration tool starts the Cryptographic Key Wizard. This makes it easy to select or create the key you need and save it to a file and to set the appropriate values in the configuration. The only page you may find confusing is the final one where you must specify either Machine mode or User mode access to the key.

You should select **Machine** mode if your application runs on its own dedicated server that is not shared with other applications, or when you have multiple applications that run on the same server and you want those applications to be able to share sensitive information.

Select **User** mode if you run your application in a shared hosting environment and you want to make sure that your application's sensitive data is not accessible to other applications on the server. In this situation, each application should run under a separate identity, and the resources for the application—such as files and databases—should be restricted to that identity.

If you add a DPAPI symmetric cryptography provider to your list of symmetric providers, you can specify the Protection Scope as either **CurrentUser** or **LocalMachine**. Current user means that DPAPI uses a loaded user profile to generate the key, and only that user account can decrypt the encrypted data. Local machine means that any code running on the machine has access to the protected key, and can decrypt any secret encrypted in the same mode.