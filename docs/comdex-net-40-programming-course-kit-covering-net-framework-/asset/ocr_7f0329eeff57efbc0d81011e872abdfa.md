**Table 5.12: Public Properties of the PasswordRecovery Class**

| Property | Description |
|---|---|
| `AnswerRequiredErrorMessage` | Using this property, a custom error message for the PasswordRecovery control can be specified in case the user leaves the answer field blank |
| `QuestionFailureText` | Using this property, a custom message for the PasswordRecovery control can be specified in case the user provides the incorrect answer |
| `SuccessText` | Using this property, a custom message for the PasswordRecovery control can be specified in case the task of password recovery is accomplished successfully |

**Table 5.13: Public Events of the PasswordRecovery Class**

| Event | Description |
|---|---|
| `AnswerLookupError` | Invoked when the user's answer to the question is found to be incorrect |
| `SendingMail` | Invoked when the server sends an e-mail containing the password after the user's answer is found to be correct |
| `VerifyingAnswer` | Invoked when the user has submitted the answer to the password-recovery confirmation question |

Now, you learn how to use the **PasswordRecovery** control in a Web site by performing the following steps:

+   1. *Click* **Start→All Programs→Microsoft Visual Studio 2010→Microsoft Visual Studio 2010**.
+   2. *Select* **File→New→Web Site** from the menu bar.  
+      The New Web Site dialog box appears.
+   3. *Select* **Visual C#** from the **Installed Templates** pane and then select the **ASP.NET Empty Web Site** template in the middle pane.
+   4. *Set* the name of the Web site as **PasswordRecoveryControl**.
+   5. *Click* the **OK** button.  
+      The **PasswordRecoveryControl** application is created.
+   6. *Open* the Solution Explorer window and right-click the application name. In this case, we are right-clicking the **PasswordRecoveryControl** application.
+   7. *Add* a Web form (**Default.aspx**) to the **PasswordRecoveryControl** application.  
+      Similarly, add another Web form (**Default2.aspx**) to the **PasswordRecoveryControl** application.
+   8. *Drag and drop* a Login control on the form (**Default.aspx**) and create a user account as done earlier.  
+      Also, set its **DestinationPageUrl** property to **Default2.aspx**.
+   9. *Drag and drop* a PasswordRecovery control from the Toolbox on the **Default2.aspx** page.
+   10. *Open* the IIS manager in your system (Fig.ASP-5.34).
+   11. *Double-click* the **Simple Mail Transfer Protocol (SMTP)** E-mail option from the ASP.NET section, as shown in Fig.ASP-5.34.