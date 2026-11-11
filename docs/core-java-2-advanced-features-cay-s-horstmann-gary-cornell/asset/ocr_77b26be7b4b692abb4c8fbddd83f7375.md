# Listing 9.20 *(Continued)*

```
```java
try (ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream(args[1])))
{
    out.writeObject(keyPair.getPublic());
}
try (ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream(args[2])))
{
    out.writeObject(keyPair.getPrivate());
}
}
else if (args[0].equals("-encrypt"))
{
    KeyGenerator keygen = KeyGenerator.getInstance("AES");
    SecureRandom random = new SecureRandom();
    keygen.init(random);
    SecretKey key = keygen.generateKey();

    // wrap with RSA public key
    try (ObjectInputStream keyIn = new ObjectInputStream(new FileInputStream(args[3]));
         DataOutputStream out = new DataOutputStream(new FileOutputStream(args[2]));
         InputStream in = new FileInputStream(args[1]) )
    {
        Key publicKey = (Key) keyIn.readObject();
        Cipher cipher = Cipher.getInstance("RSA");
        cipher.init(Cipher.WRAP_MODE, publicKey);
        byte[] wrappedKey = cipher.wrap(key);
        out.writeInt(wrappedKey.length);
        out.write(wrappedKey);

        cipher = Cipher.getInstance("AES");
        cipher.init(Cipher.ENCRYPT_MODE, key);
        Util.crypt(in, out, cipher);
    }
}
else
{
    try (DataInputStream in = new DataInputStream(new FileInputStream(args[1]));
         ObjectInputStream keyIn = new ObjectInputStream(new FileInputStream(args[3]));
         OutputStream out = new FileOutputStream(args[2]))
    {
        int length = in.readInt();
        byte[] wrappedKey = new byte[length];
        in.read(wrappedKey, 0, length);

        // unwrap with RSA private key
        Key privateKey = (Key) keyIn.readObject();

        Cipher cipher = Cipher.getInstance("RSA");
```
```