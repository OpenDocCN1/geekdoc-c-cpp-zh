Partition. In this way, searching the Vancouver directory would list only users assigned to the Vancouver Partition.

# Describe Cisco Unity Connection Users and Mailboxes

The system components identified previously are important, but without users and mailboxes, system functionality is limited. The following sections outline the basics of adding users and mailboxes to the system.

# User Templates

User Templates, as the name implies, provide a pattern used in the creation of new user accounts. Most of the required configuration information common to all the new users can be entered in the template, and then the individual user-specific information is combined with the template to create (potentially) new user accounts with speed and accuracy. The template settings are applied as the user is created; changing the template not retroactively change the user accounts that were created using that template.

Two default User Templates are created at install: one for administrators and one for users. These can be modified if desired, and as many custom templates as needed can be created.

The following sections highlight some of the settings on the User Template Pages (of which there are many, so not all settings are discussed).

# User Template Basics

The basic elements of User Template configuration are summarized in the following sections:

+   **Name:** The name of the template, such as Managers. The Alias and Display Name generation for user accounts can also be specified; the default is first name followed by last name.

+   **Phone:** In this section, the Dial-Plan (Partition/Search Space), Class of Service (CoS), and Schedule are defined.

+   **Location:** Geographic location information, language localization, and time zone are set here.

> **Key Point:** CoS in CUC (not to be confused with Layer 2 Quality of Service [QoS] marking or CCM Class of Control) is a simple and powerful method of assigning and restricting user privilege. The CoS defines greeting and message length timers, licensed feature access, advanced feature access, alternate extension definition, Private DL number, and membership limits and call transfer abilities.

An unlimited number of CoS can be defined, providing exactly the combination of abilities and features for as many sets of users as needed.

![](bbox=[0.878, 0.705, 0.943, 0.765])