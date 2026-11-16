configuration. Following the basic principles defined in the beginning of the chapter, there must be zero operational overhead for customers when running a partner extension as part of their SuccessFactors system. We'll leave it up to you to judge that. We'll point you to a practical example from SAP you can explore on your own, and we'll also iterate over the APIs and possible integration points available for your extension application to leverage.

# 11.4.1 SuccessFactors Administration Layers

The first thing to keep in mind is that SuccessFactors has two separate layers of administration externally visible:

+   SuccessFactors Provisioning is used for trained SuccessFactors implementation consultants and SuccessFactors professional services consultants.

+   SuccessFactors OneAdmin is used by company account administrators and key users.

There is a clear difference between these two roles, which we discuss next.

# SuccessFactors Provisioning

SuccessFactors Provisioning is the environment used to configure all the licensed features of the SuccessFactors product. This includes enabling the required modules, configuration, mapping the company business processes to workflows, enabling API access, adding new administration users, and so on. Regular recurring replication jobs are also configured and scheduled in Provisioning.

The general trend is to grow the set of features exposed to key users and company administrators, enabling them to handle the company accounts they are responsible for. At the same time, critical operations will still remain in SuccessFactors Provisioning, where company admins have no access. If any configuration changes are required there, then such changes would be performed either by an implementation consultant or by SuccessFactors professional service teams.

The point here is not that SAP does not want to provide access to customers. It's about making sure that only people with the required qualifications, background, and skills will make low-level configuration changes to customer systems. That's one approach to minimize the risk of destabilizing the account and the productive business processes there.