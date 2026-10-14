# The directory structure

Figure 19-16 shows the directory structure for the Authentication application. This shows the App_Data folder that stores the SQL Server Express database that’s used to store the data about the web site’s registered users and their roles. In addition, it shows two directories that store web pages that have restricted access. First, it shows the Maintenance directory, which contains the Maintenance page shown in the previous figure. Second, it shows the MyAccount directory, which contains the MyAccount page shown in the previous figure.

In addition, there are three web.config files for this application: one for the root directory, one for the Maintenance directory, and one for the MyAccount directory. The complete listings for these files are shown in figure 19-17.

# The access rules

Figure 19-16 also shows the one access rule for the MyAccount directory. This rule denies access to anonymous users. As a result, only users who are authenticated can access the MyAccount directory.

The Maintenance directory, on the other hand, contains two access rules. The first rule denies access to all users. Then, the second rule allows access to authenticated users who are associated with the admin role. To refresh your memory about how this works, please refer back to figure 19-7.