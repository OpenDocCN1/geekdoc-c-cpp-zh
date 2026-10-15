```
"Q1/IWoraddTH3IXAUQJGDSYDQcYYu0pm"
Private Shared b64IVs() As String = ("onQX8hdHeWQ=", _
"jgetiyz+PlC=", _
"pd5mgMmfDI2Gxm/SK1I5A==", _
"6jpFrUh8FF4=")

Public Shared Sub Main(ByVal textBox As TextBox, ByVal algoIndex As Integer,
    ByVal inputFile As String, ByVal outputFile As String,
    ByVal encryptFile As Boolean)

    Dim fin As FileStream = File.OpenRead(inputFile)
    Dim fout As FileStream = File.OpenWrite(outputFile)
    Dim sa As SymmetricAlgorithm = SymmetricAlgorithm.Create(algo(algoIndex))
    sa.IV = Convert.FromBase64String(b64IVs(algoIndex))
    sa.Key = Convert.FromBase64String(b64Keys(algoIndex))
    textBox.Text = "Key length: " & CType(sa.Key.Length, String) & Environment.NewLine
    textBox.Text &= "Initial Vector length: " & CType(sa.IV.Length, String) & Environment.NewLine
    textBox.Text &= "KeySize: " & CType(sa.KeySize, String) & Environment.NewLine
    textBox.Text &= "BlockSize: " & CType(sa.BlockSize, String) & Environment.NewLine
    textBox.Text &= "Padding: " & CType(sa.Padding, String) & Environment.NewLine
    If (encryptFile) Then
        Encrypt(sa, fin, fout)
    Else
        Decrypt(sa, fin, fout)
    End If
End Sub
```

Code snippet from SyncEnc.vb

The parameters to Main provide the Textbox where the output will be displayed and the index from the array algo, which is the name of the algorithm to be used. It then looks for the input and output files, and finally a Boolean indicating whether the input should be encrypted or decrypted.

Within the code, first the action is to open the input and output files. The code then creates an instance of the selected algorithm and converts the initial vector and key strings for use by the algorithm. Symmetric algorithms essentially rely on two secret values: one called the key; the other, the initial vector, both of which are used to encrypt and decrypt the data. Both private values are required for either encryption or decryption.

The code then outputs some generic information related to the encryption being used and then checks which operation is required, executing the appropriate static method to encrypt or decrypt the file.

To encrypt, the code gets an instance of the ICryptoTransform interface by calling the CreateEncryptor method of the SymmetricAlgorithm class extender. The encryption itself is done in the following method:

```
Private Shared Sub Encrypt(ByVal sa As SymmetricAlgorithm, _
ByVal fin As Stream, _
ByVal fout As Stream)
    Dim trans As ICryptoTransform = sa.CreateEncryptor()
    Dim buf() As Byte = New Byte(fin.Length) {}
    Dim cs As CryptoStream = _
    New CryptoStream(fout, trans, CryptoStreamMode.Write)
    Dim Len As Integer
    fin.Position = 0
    Len = fin.Read(buf, 0, buf.Length)
    While (Len > 0)
        cs.Write(buf, 0, Len)
        Len = fin.Read(buf, 0, buf.Length)
    End While
    cs.Close()
```