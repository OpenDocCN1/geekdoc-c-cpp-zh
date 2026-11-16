Figure 6.42 shows the Mail destination that we configured for our sample scenario. As you can see, we've named our destination Session and assigned it the type Mail. Aside from these main properties, we've also specified a number of additional properties that are required to establish a connection to the target SMTP server: SMTP host and port, authentication parameters, protocol (SMTP), and so on.

![](bbox=[0.15, 0.23, 0.94, 0.76])

# Figure 6.42 Creating a Mail Destination in SAP HCP Cockpit

Whenever the destination is saved, the parameters are used to create a javax.mail.Session object that gets stored in the Java EE container's JNDI context under the mail/<Destination Name> context path (e.g., mail/Session in our