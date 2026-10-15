
```
Public Sub Main(ByVal CmdArgs() As String)
    Dim keyz As StringBuilder = New StringBuilder
    Dim ivz As StringBuilder = New StringBuilder
    keyz.Append("Dim b64Keys() As String = { _" + vbCrLf)
    ivz.Append(vbCrLf + "Dim b64IVs() As String = { _" + vbCrLf)
    Dim comma As String = "," & _
        vbCrLf
    Dim algo() As String = {"DES", "RC2", "Rijndael", "TripleDES"}
    For i As Integer = 0 To 3
        Dim sa As SymmetricAlgorithm = SymmetricAlgorithm.Create(algo(i))
        sa.GenerateIV()
        sa.GenerateKey()
        Dim Key As String
        Dim IV As String
        Key = Convert.ToBase64String(sa.Key)
        IV = Convert.ToBase64String(sa.IV)
        keyz.AppendFormat(vbTab + "\""" + Key + "\""" + comma)
        ivz.AppendFormat(vbTab + "\""" + IV + "\""" + comma)
        If i = 2 Then comma = " "
    Next i
    keyz.Append("}")
    ivz.Append("}")
    Console.WriteLine(keyz.ToString())
    Console.WriteLine(ivz.ToString())
End Sub
End Class
```

Code snippet from SymEnc.vb

The preceding program creates a random key and an initializing vector for each algorithm. The output from this can be copied into the SymEnc.vb program.

## PKCS

The Public Key Cryptographic System (PKCS) is a type of asymmetric key encryption. This system uses two keys, one private and the other public. The public key is widely distributed, whereas the private key is kept secret. One cannot derive or deduce the private key by knowing the public key, so the public key can be safely distributed.

The keys are different, yet complementary. That is, if you encrypt data using the public key, then only the owner of the private key can decipher it, and vice versa. This forms the basis of PKCS encryption.

If the private key holder encrypts a piece of data using his or her private key, any person with access to the public key can decrypt it. The public key, as the name suggests, is available publicly. This property of the PKCS is exploited along with a hashing algorithm, such as SHA or MD5, to provide a verifiable digital signature process.

The abstract class System.Security.Cryptography.AsymmetricAlgorithm represents this concept in the .NET Framework. Four concrete implementations of this class are provided by default:

- DSACryptoServiceProvider, which extends the abstract class DSA
- ECDiffieHellmanCng, which extends the ECDiffieHellman abstract class
- ECDsaCng, which extends the abstract class ECDsa
- RSACryptoServiceProvider, which extends the abstract class RSA

The Digital Signature Algorithm (DSA) was specified by the National Institute of Standards and Technology (NIST) in January 2000. The original DSA standard, however, was issued by NIST much earlier, in August 1991. DSA cannot be used for encryption and is good only for digital signature. Digital signature is discussed in more detail in the next section.

Similarly, the ECDsa algorithm is also an elliptic curve algorithm, in this case combined with the Digital Signature Algorithm. This is then enhanced with a Cryptographic Next Generation algorithm.

RSA algorithms can also be used for encryption as well as digital signatures. RSA is the de facto standard and has much wider acceptance than DSA. RSA is a tiny bit faster than DSA as well.

RSA can be used for both digital signature and data encryption. It is based on the assumption that large numbers are extremely difficult to factor. The use of RSA for digital signatures is approved within the FIPS PUB 186-2 and is defined in the ANSI X9.31 standard document.

## Digital Signature Example

Digital signature is the encryption of a hash digest (for example, MD5 or SHA-1) of data using a private key. The digital signature can be verified by decrypting the hash digest and comparing it against a hash digest computed from the data by the verifier.

As noted earlier, the private key is known only to the owner, so the owner can sign a digital document by encrypting the hash computed from the document. The public key is known to all, so anyone can verify the signature by recomputing the hash and comparing it against the decrypted value, using the public key of the signer.

The .NET Framework provides DSA and RSA digital signature implementations by default. This section considers only DSA, as both implementations extend the same base class, so all programs for DSA discussed here work for RSA as well.

First, you need to produce a key pair. To do this, you’ll need the following method, which has been added to the ProVB_Security main form. It can be called once from the ButtonTest click event to generate the necessary files in your application’s folder:

```
Private Sub GenDSAKeys()
    Dim dsa As DSACryptoServiceProvider = New DSACryptoServiceProvider
    Dim prv As String = dsa.ToXmlString(True)
    Dim pub As String = dsa.ToXmlString(False)
    Dim fileutil As FileUtil = New FileUtil
    fileutil.SaveString("dsa-key.xml", prv)
    fileutil.SaveString("dsa-pub.xml", pub)
End Sub
```

Code snippet from Form1.vb

This method generates two XML-formatted files, dsa-key.xml and dsa-pub.xml, containing private and public keys, respectively. This code is dependent on an additional class, FileUtil that is available in the project to wrap some of the common file I/O operations. This file is shown in the following code snippet:

```
'FileUtil.vb
Imports System.IO
Imports System.Text
Public Class FileUtil
    Public Sub SaveString(ByVal fname As String, ByVal data As String)
        SaveBytes(fname, (New ASCIIEncoding).GetBytes(data))
    End Sub
    Public Function LoadString(ByVal fname As String)
        Dim buf() As Byte = LoadBytes(fname)
        Return (New ASCIIEncoding).GetString(buf)
    End Function
    Public Function LoadBytes(ByVal fname As String)
        Dim finfo As FileInfo = New FileInfo(fname)
        Dim length As Long = CType(finfo.Length, Long)
        Dim buf() As Byte = New Byte(length) {}
        Dim fs As FileStream = File.OpenRead(fname)
        fs.Read(buf, 0, buf.Length)
        fs.Close()
        Return buf
    End Function
    Public Sub SaveBytes(ByVal fname As String, ByVal data() As Byte)
        Dim fs As FileStream = File.OpenWrite(fname)
        fs.SetLength(0)
        fs.Write(data, 0, data.Length)
        fs.Close()
    End Sub
    Public Function LoadSig(ByVal fname As String)
        Dim fs As FileStream = File.OpenRead(fname)
        ' Need to omit the trailing null from the end of the 0 based buffer.
        Dim buf() As Byte = New Byte(39) ()
        fs.Read(buf, 0, buf.Length)
        fs.Close()
        Return buf
    End Function
End Class
```

Code snippet from FileUtil.vb

To create the signature for a data file, reference the DSASign class from the ButtonTest click event handler. The following code signs the data:

```
'DSASign.vb
Imports System
Imports System.IO
Imports System.Security.Cryptography
Imports System.Text

Public Class DSASign
    Public Shared Sub Main()
        Dim fileutil As FileUtil = New FileUtil
        Dim xkey As String = fileutil.LoadString("dsa-key.xml")
        Dim fs As FileStream = File.OpenRead("..\..\FileUtil.vb")
        Dim data(fs.Length) As Byte
        fs.Read(data, 0, fs.Length)
        Dim dsa As DSACryptoServiceProvider = New DSACryptoServiceProvider
        dsa.FromXmlString(xkey)
        Dim sig() As Byte = dsa.SignData(data)
        fs.Close()
        fileutil.SaveBytes("FileUtilSignature.txt", sig)
    End Sub
End Class
```

Code snippet from DSASign.vb

Now that you have a data file and a signature, the next step is to verify the signature. The class DSAVerify can be leveraged to verify that the signature file created is in fact valid:

```
'DSAVerify.vb
Imports System
Imports System.IO
Imports System.Security.Cryptography
Imports System.Text

Public Class DSAVerify
```
