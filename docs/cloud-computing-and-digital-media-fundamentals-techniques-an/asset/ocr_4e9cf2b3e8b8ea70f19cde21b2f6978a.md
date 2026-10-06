The system in this chapter implements the learning center based on the GAE architecture and uses the resources in GAE to provide related educational service that we design.
The main services of the learning center are as follows:

+   * Identification of user
* Storage of learning progress
* Course data management
* Course database

To satisfy the requirements, this research divides the learning center into the following modules:

+   * User management module
* Learning progress recording module
* Course data access module
* Course data management module

In the next section, we will discuss about these modules and the problems that are met and how the research solves those problems.

# 6.3.1.1 User Management Module

This module is responsible for managing the accounts of the user such as adding, deleting, and modifying the permissions of the user accounts. Learning center uses this module to decide the permissions in the system and manage the identity of the user by permissions control. The identification of the user in the learning center can simply be divided into two categories: teachers and students. Teachers in the learning center have a greater authority to manage the accounts, access the functions in the system, and use the course data management module to set the access permissions of each course. Students in the learning center have less permission in the system. Both of these identities use this module to maintain the personal data.

In addition, the devices that each user uses must be different; some users may use PC or NB at home but they use smart phone or tablet PC when they are outside of the home. Hence, this module will record the device type and number to recognize all learning devices. The learning