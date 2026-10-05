+   Minimum API Level: The lowest version of Android the game will run on. You’ll need to download the SDK version of the version you choose here. Most devices have version 4.4 or higher, so it’s a good idea to leave it at 4.4. If you need specific functionality from the Android system that requires a higher version, be sure to adjust this value.

Open the Publishing Settings module:

| Publishing Settings | |
| --- | --- |
| Keystore | [x] Existing Keystore [ ] Create a new keystore |
| | Browse Keystore D:/Android/keystore/black |
| Keystore password | |
| Confirm keystore password | |
| Enter password. | |
| Key | blackdragonbe |
| Password | |
| Enter password. | |

Here’s where you choose or create a keystore. The keystore is used to authenticate your apps and games. It’s a certificate to prove that you are the developer. If you already created a key, simply click Browse Keystore to find your keystore file, then enter the password.

Now, select or create the Alias you want to use, enter its password and you’re good to go!

If you don’t have a keystore, select Create New Keystore, click Browse Keystore and choose a location to save the keystore. Now choose a password for the keystore and create an alias and its password.

You’re now ready to make an Android build!

Open the Build window and either click Build And Run, if you have an Android device attached to the build immediately, or click Build to simply create an APK (Android Application Package). Either way, you’ll have to choose a name and location to put the resulting APK.

Once you do, the editor will build and compile all assets into an Android package, and copy and install it if you chose Build And Run. Be sure to remember where you chose to put the APK as you’ll need it soon.