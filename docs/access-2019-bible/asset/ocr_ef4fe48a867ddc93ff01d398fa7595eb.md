# Chapter 31: Preparing Your Access Application for Distribution

+   1. Open the Visual Basic Editor by pressing Alt+F11.
+   2. In the Visual Basic Editor, choose Tools → Chapter31 Properties. The Project Properties dialog box appears.
+   3. Select the Protection tab (shown in Figure 31.23).

![](bbox=[0.186, 0.246, 0.894, 0.577])

+   4. Select the Lock Project for Viewing check box.
+   5. Enter a password in the Password text box. Access does not display the password; instead, it shows a dot for each letter.
+   6. Type the password again in the Confirm Password text box and click OK. This security measure ensures that you don’t mistype the password (because you can’t see the characters that you type) and mistakenly prevent everyone, including yourself, from accessing the database.

After you save and close the project, users attempting to view the application’s code must enter the password. Access prompts for the project password only once per session.

A more secure method of securing your application’s code, forms, and reports is to distribute your database as an ACCDE file. When you save your database as an ACCDE file, Access compiles all code modules (including form modules), removes all editable source code, and compacts the database. The new ACCDE file contains no source code but continues to work