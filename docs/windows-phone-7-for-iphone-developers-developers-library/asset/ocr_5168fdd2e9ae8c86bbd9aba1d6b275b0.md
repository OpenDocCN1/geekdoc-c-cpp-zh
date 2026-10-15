instance of Rfc2898DeriveBytes. The specific size of the key and IV are recommendations from Microsoft. Again, if you're looking for a more in-depth discussion of why these values are the way they are, check out the MSDN documentation on encryption and security or consult your favorite book on encryption algorithms.

Next you'll see I'm using the cryptoStream class. This class takes constructor arguments a stream (in our case a memory stream), an encryptor or decryptor, and finally an enum value indicating whether the stream is being opened for reading or writing. This is an incredibly handy class because after you have a cryptoStream, it automatically takes care of encrypting or decrypting for you. Data that is written to a cryptographic stream is automatically processed by the encryption provider. As you can see in Listing 19.1, we use the CreateEncryptor() and CreateDecryptor() methods of the AesManaged class to create streams that either encrypt or decrypt data that is written to the stream.

Last, you might see something that we covered in the chapter on isolated storage. We're using the IsolatedStorageSettings class to read and write application settings. In this case, the setting is encrypted so that even if the application and the phone were to be compromised, the data salvaged by a hacker would be useless without the password and the salt, which are not stored anywhere on the device. You don't have to use this class, you can use the IsolatedStorageFile class to read and write entire object graph hierarchies in encrypted format, ensuring that every single piece of data in your model is secure.

```
Listing 19.1 MainPage.xaml.cs Encrypting and Decrypting Data

using System;
using System.Windows;
using Microsoft.Phone.Controls;
using System.Security.Cryptography;
using System.IO;
using System.Text;
using System.IO.IsolatedStorage;

namespace EncryptionSample
{
  public partial class MainPage : PhoneApplicationPage
  {
    // Constructor
    public MainPage()
    {
      InitializeComponent();
    }

    private AesManaged GetAesWithKey(string password, string salt)
    {
      AesManaged aes = new AesManaged();
      Rfc2898DeriveBytes keySource =
        new Rfc2898DeriveBytes(password, Encoding.UTF8.GetBytes(salt));
    }
  }
}
```