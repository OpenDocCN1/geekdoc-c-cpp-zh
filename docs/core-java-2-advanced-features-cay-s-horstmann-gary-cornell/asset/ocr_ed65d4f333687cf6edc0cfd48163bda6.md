| `javax.crypto.KeyGenerator` | `1.4` |
|---|---|
| • `static KeyGenerator getInstance(String algorithmName)`<br>returns a KeyGenerator object that implements the specified algorithm. Throws a `NoSuchAlgorithmException` if the algorithm is not provided.<br><br>• `void init(SecureRandom random)`<br>• `void init(int keySize, SecureRandom random)`<br>initializes the key generator.<br><br>• `SecretKey generateKey()`<br>generates a new key. |

| `javax.crypto.spec.SecretKeySpec` | `1.4` |
|---|---|
| • `SecretKeySpec(byte[] key, String algorithmName)`<br>constructs a key specification. |

# ### 9.5.3 Cipher Streams

The JCE library provides a convenient set of stream classes that automatically encrypt or decrypt stream data. For example, here is how you can encrypt data to a file:

```
Cipher cipher = ... ;
cipher.init(Cipher.ENCRYPT_MODE, key);
CipherOutputStream out = new CipherOutputStream(new FileOutputStream(outputFileName), cipher);
byte[] bytes = new byte[BLOCKSIZE];
int inLength = getData(bytes); // get data from data source
while (inLength != -1)
{
    out.write(bytes, 0, inLength);
    inLength = getData(bytes); // get more data from data source
}
out.flush();
```

Similarly, you can use a CipherInputStream to read and decrypt data from a file:

```
Cipher cipher = ... ;
cipher.init(Cipher.DECRYPT_MODE, key);
CipherInputStream in = new CipherInputStream(new FileInputStream(inputFileName), cipher);
byte[] bytes = new byte[BLOCKSIZE];
int inLength = in.read(bytes);
while (inLength != -1)
{
```