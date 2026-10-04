# Processing Data at the Server | 331

![](bbox=[0.15358000000000002, 0.10353, 0.65642, 0.41255000000000003])

# How It Works

The mail-sending part of this exercise is pretty similar to the demo page you created earlier. What’s different, however, is where the body text for the mail message comes from. Instead of hard-coding the body in the Code Behind of the FormControl control, you moved the text to a separate file. This file contains few placeholders that are replaced at run with the user’s details. To read the entire file in one, use the following code:

# VBNET

```
Dim fileName As String = Server.MapPath("/App_Data/ContactForm.txt")
Dim mailBody As String = File.ReadAllText(fileName)
```

# C#

```
string fileName = Server.MapPath("/App_Data/ContactForm.txt")
string mailBody = File.ReadAllText(fileName);
```

The first lines use Server.MapPath to translate a virtual path into its physical counterpart because it doesn't depend on any hard-coded paths. By using the virtual path, it's easier to move your site to a different location because Server.MapPath("/App_Data/ContactForm.txt") returns a physical path such as C:\BegASPNET\Site\App_Data\ContactForm.txt. This path is then found to the ReadAllText method of the File class, which opens the file and returns its contents, which are then assigned to the mail-Body variable.