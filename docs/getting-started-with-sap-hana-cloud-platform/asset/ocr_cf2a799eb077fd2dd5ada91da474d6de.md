IdPs as well. We'll be exploring the implications of all this in greater detail in Section 8.5, but for now the primary takeaway of all this is that user accounts are defined outside of SAP HCP.

To simplify the role assignment process a bit further, SAP HCP also allows you to define custom *groups* that combine multiple roles together so that they can be assigned to particular classes of users in one go. For the most part, the process of assigning a user to a group is identical to the process used to assign roles. Of course, before you can do that, you have to first define the group(s) themselves.

Unlike user accounts, which are maintained within the external IdP, groups are defined within the context of an SAP HCP account in the SAP HCP Cockpit. From the top-level AUTHORIZATIONS tab page, you can get to the group editor by clicking on the Groups subtab (Figure 8.7).

![](bbox=[0.156, 0.406, 0.856, 0.773])

Figure 8.7 Defining Groups in the SAP HCP Cockpit

To create a new group record, simply plug the group name into the Group field and then click on the SHOW ASSIGNMENTS button. With the new group record staged, you can begin adding roles to the group using the roles table shown on