# SUMMARY

You can implement security in your ASP.NET site with several techniques, including Windows authentication (where the web server takes care of authentication) and Forms authentication, which is the de facto standard for many of today's ASP.NET websites.

In general, security encompasses three important components: identity, authentication, and authorization. Together, they determine who you are and what you are allowed to do.

The Membership service (that uses a Membership provider under the hood) enables you to create and manage users in a central database using controls such as CreateUserWizard, PasswordRecovery, and Login.

The Role Manager (which uses a Role provider under the hood) enables you to group users in various roles to which you can assign permissions. You can check roles programmatically, or use the LoginView to present different data depending on the role the user is assigned to.

Users and roles are managed with the WSAT, so you can assign user accounts to different roles, as you see in this chapter. You can then open or block specific resources in your website to members in a certain role using <location> elements in the Web.config file.

The various login controls enable you to customize the content that users get to see. In the next chapter you discover how to take this one level further, by creating dynamic pages that adapt based on the user that is accessing them.

# EXERCISES

+   1. What's the difference between authentication and authorization?

+   2. Right now the Management folder is blocked for all users except those in the Managers role. What do you change to need to make the Web.config file if you also want to open up the folder for the user John and all people in the Editors role?

+   3. Imagine you have a feature that has a Login page with a single Login control. What change to the Login control do you need to make to send users to MyProfile.aspx in the root after they log in?

+   4. What's the difference between the LoginView and LoginStatus controls? When would you use each one?

You can find answers to these exercises in Appendix A.