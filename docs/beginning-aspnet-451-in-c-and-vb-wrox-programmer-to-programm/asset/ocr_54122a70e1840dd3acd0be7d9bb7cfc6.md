The following table lists the most common methods of the File class that enable you to work with files.

| METHOD | VALUE |
|---|---|n| AppendAllText | Appends a specified string to a text file. If the file does not exist, it's created first. |
| Copy | Copies a file from one location to another. |
| Delete | Deletes the specified file from disk. |
| Exists | Checks if the specified file exists on disk. |
| Move | Moves the specified file to a different location. |
| ReadAllText | Reads the contents of a text file. |
| WriteAllText | Writes the contents of a string to a new file and overwrites the target if it already exists. |

You can use these methods for all kinds of purposes. For example, when you have uploaded a file, you can use the Move method to move it to a different folder. Additionally, when you want to rid of uploaded files that you don't need, use the Delete method.

The ReadAllText method is used to read the complete contents of a text file. For example, when sending text by e-mail, you could store the body text of the e-mail in a text file. When you're about to send the e-mail, you call ReadAllText and assign the contents that this method returns to the body of the e-mail. You see how this works in the following Try It Out.

# TRY OUT Sending Mail from the ContactForm User Control

This exercise shows how to use e-mail to send the data from the contact form to your own Inbox. As the body of the e-message, the code reads in a text file that contains placeholders. These placeholders are filled with the actual user data from the source.

+   1. Start by adding a new text file to the App_Data folder in your website. If you don't have the App_Data folder yet, right-click the website and choose Add ASP.NET Folder Add App_Data. Create the text file by right-clicking the App_Data folder and choosing Add New Item. Select Text File, name the file ContactForm.txt, and click Add.

+   2. Enter the following text in the file, including the placeholders wrapped in a pair of double symbols:
Hi there,
A user has left the following feedback at the site:

```
##Name##nE-mail address: ##Email##nHome phone: ##HomePhone##nBusiness phone: ##BusinessPhone##nComments: ##Comments##
```