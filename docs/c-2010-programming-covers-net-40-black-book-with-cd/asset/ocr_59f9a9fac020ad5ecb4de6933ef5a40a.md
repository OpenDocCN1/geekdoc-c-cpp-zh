# Table 16.11: Noteworthy Properties of the PasswordRecovery Class

| Property | Description |
|---|---|
| SuccessTemplate | Retrieves or specifies the template for the PasswordRecovery control when it is in the Success view |
| SuccessText | Specifies a custom message for the PasswordRecovery control to be displayed in case the task of password recovery is accomplished successfully |
| SuccessTextStyle | Retrieves or specifies the style in which the Success text is to be displayed |
| UserName | Retrieves or specifies the text to be displayed in the User Name text box |
| UserNameFailureText | Retrieves or specifies the text when a user enters an invalid username |
| UserNameInstructionText | Retrieves or specifies the text in the PasswordRecovery control when it is in the UserName view |
| UserNameLabelText | Retrieves or specifies the label for the User Name text box |
| UserNameRequiredErrorMessage | Retrieves or specifies the error message that is displayed when a user does not enter any value in the User Name text box |
| UserNameTemplate | Retrieves or specifies the template used to display the UserName view of the PasswordRecovery control |
| UserNameTitleText | Retrieves or specifies the title of the PasswordRecovery control when it is in the UserName view |
| ValidatorTextStyle | Retrieves or specifies the style properties that are used to define the look of the error message of the Validator control |

Table 16.12 lists the noteworthy events of the PasswordRecovery class:

# Table 16.12: Noteworthy Events of the PasswordRecovery Class

| Event | Description |
|---|---|
| AnswerLookupError | Initiated when the user enters an incorrect answer to the question during password recovery information |
| SendingMail | Initiated when the server is sending an e-mail containing the password after the user requests a new or recovered password after submitting the correct answer to the question |
| SendMailError | Initiated when the SMTP Mail system throws an error while attempting to send an e-mail message |
| UserLookupError | Initiated when the Membership provider cannot find the username entered by the user |
| VerifyingAnswer | Initiated when the user has submitted the answer to the password recovery confirmation question |
| VerifyingUser | Initiated when the validation of username by the Membership provider is under process |

You can simply drag-and-drop this control from the Toolbox to add it to a Web page.

Figure 16.6 displays the PasswordRecovery control at design time: