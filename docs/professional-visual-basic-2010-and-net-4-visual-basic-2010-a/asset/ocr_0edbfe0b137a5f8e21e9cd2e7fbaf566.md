![](bbox=[0.09, 0.087, 0.75, 0.45])

# FIGURE 20-4

Visual Studio will create an App_Data folder and place your database in it. Now double-click your database and add two tables, beginning with the Customers table shown in Table 20-1.

# TABLE 20-1: Customers

| COLUMN NAME | TYPE | DESCRIPTION |
|---|---|---|
| CustomerID | Int | Unique identity for customers |
| Name | Varchar (50) | Name of customer |
| PhoneNumber | Varchar (50) | Phone number of customer |
| EMailAddress | Varchar (50) | E-mail address of customer |
| Address | Varchar (50) | Address of customer |
| City | Varchar (50) | City of customer |
| State | Varchar (50) | State of customer |

Now that we have a customer table, we’ll also add an Issues table to keep track of issues for the customer. This will build a basic issue-tracking database. Add the structure for the Issues table as shown in Table 20-2.

# TABLE 20-2: Issues

| COLUMN NAME | TYPE | DESCRIPTION |
|---|---|---|
| IssueID | Int | Unique identity for issues |
| CustomerID | Int | ID of customer to whom the issue belongs |
| IssueDate | Datetime | Date of issue |
| ResolvedDate | Datetime | Date the issue was resolved |
| Description | Varchar (5000) | Description of issue |
| Resolution | Varchar (5000) | Resolution of issue |