```
```java
public void loadFile(String filename)
{
    fileText.setText("");
    try
    {
        fileText.append(new String(Files.readAllBytes(Paths.get(filename))));
    }
    catch (IOException ex)
    {
        fileText.append(ex + "\n");
    }
    catch (SecurityException ex)
    {
        fileText.append("I am sorry, but I cannot do that.\n");
        fileText.append(ex + "\n");
        ex.printStackTrace();
    }
}
```
```

# ## 9.5 Encryption

So far, we have discussed one important cryptographic technique implemented in the Java security API—namely, authentication through digital signatures. A second important aspect of security is encryption. Even when authenticated, the information itself is plainly visible. The digital signature merely verifies that the information has not been changed. In contrast, when information is encrypted, it is not visible. It can only be decrypted with a matching key.

Authentication is sufficient for code signing—there is no need to hide the code. However, encryption is necessary when applets or applications transfer confidential information, such as credit card numbers and other personal data.

In the past, patents and export controls prevented many companies from offering strong encryption. Fortunately, export controls are now much less stringent, and the patents for important algorithms have expired. Nowadays, Java SE has excellent encryption support as a part of the standard library.

# ### 9.5.1 Symmetric Ciphers

The Java cryptographic extensions contain a class `Cipher` that is the superclass of all encryption algorithms. To get a cipher object, call the `getInstance` method:

```
```java
Cipher cipher = Cipher.getInstance(algorithmName);
```
```

or