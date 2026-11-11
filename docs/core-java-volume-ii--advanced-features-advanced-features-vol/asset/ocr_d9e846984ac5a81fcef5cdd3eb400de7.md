| javax.crypto.KeyGenerator 1.4 (Continued) |
| --- |
| • `SecretKey generateKey()`<br>generates a new key. |

| javax.crypto.spec.SecretKeySpec 1.4 |
| --- |
| • `SecretKeySpec(byte[] key, String algorithmName)`<br>constructs a key specification. |

# ### 10.5.3 Cipher Streams

The JCE library provides a convenient set of stream classes that automatically encrypt or decrypt stream data. For example, here is how you can encrypt data to a file:

```
```java
Cipher cipher = . . .;
cipher.init(Cipher.ENCRYPT_MODE, key);
var out = new CipherOutputStream(new FileOutputStream(outputFileName), cipher);
var bytes = new byte[BLOCK_SIZE];
int inLength = getData(bytes); // get data from data source
while (inLength != -1)
{
    out.write(bytes, 0, inLength);
    inLength = getData(bytes); // get more data from data source
}
out.flush();
```
```

Similarly, you can use a CipherInputStream to read and decrypt data from a file:

```
```java
Cipher cipher = . . .;
cipher.init(Cipher.DECRYPT_MODE, key);
var in = new CipherInputStream(new FileInputStream(inputFileName), cipher);
var bytes = new byte[BLOCK_SIZE];
int inLength = in.read(bytes);
while (inLength != -1)
{
    putData(bytes, inLength); // put data to destination
    inLength = in.read(bytes);
}
```
```

The cipher stream classes transparently handle the calls to update and doFinal,
which is clearly a convenience.