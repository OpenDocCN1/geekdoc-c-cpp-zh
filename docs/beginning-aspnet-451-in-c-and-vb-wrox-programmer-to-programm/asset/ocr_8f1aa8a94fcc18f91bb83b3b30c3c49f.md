# 604 | CHAPTER 16 SECURITY IN YOUR ASP.NET WEBSITE

At run time, the {} is replaced with the user's name.

By default, the LoginStatus displays a link to enable users to log in and log out. Because the Menu or the TreeView already contains a link to the Login page, the footer uses a LoginView again to display the Logout text when the user is logged in. If you want to add a Login link as well, you can extend the LoginView with an anonymous template and an additional LoginStatus or remove the entry LoginView so the LoginStatus is visible to all users.

In addition to the controls you have that enable a user to log in and that use the current user's log-status to show or hide relevant content, the Login category of the TextBox contains more controls that enable users to sign up for a new account on the site, to change an existing password, and to recover a lost password. These controls are discussed next.

# CreateUserWizard

You briefly say CreateUserWizard at work in an earlier exercise. The control has a lot more to offer than the standard behavior you see in that.

To start with, the control has a long list of Text properties, such as CancelButtonText, CompleteSuccessText, UserNameLabelText, and CreateUserButtonText, that affect the text used in the control. All properties have good (English) defaults, but you can change them if they don't suit your needs.

The control has a bunch of properties that end in ImageUrl, such as CreateUserButtonImageUrl. If you want to generate images for various users instead of buttons that the control generates. You also need to set the corresponding ButtonType. To change the CreateButton to an image, you need to set the CreateUserButtonImageUrl to a valid image and set CreateUserButtonType to Image.

The default value for the ButtonType is Button, which renders standard buttons by default. You can also set the ButtonType to Link to have them rendered as standard LinkButton controls. The associated text properties introduced at the beginning of this section are displayed on the buttons and the links.

Additionally, the control exposes a number of useful properties that you can set to change its behavior and appearance, shown in the following table.

| PROPERTY | DESCRIPTION |
| --- | --- |
| ContinueDestinationPageUrl | Defines the page where users are taken when they click Continue after signing up. |
| DisableCreatedUser | Determines whether or not the user is marked as disabled when the account is created. When set to True, users cannot log in to the site until their account has been enabled. You see how to activate and deactivate accounts manually later. Defaults to False. |