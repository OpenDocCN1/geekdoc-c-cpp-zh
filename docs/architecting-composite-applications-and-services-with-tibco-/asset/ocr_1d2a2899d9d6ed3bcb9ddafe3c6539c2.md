# Substation ES

Substation ES is a z/OS-hosted component that enables program-to-program interaction. It supports interaction both to and from the mainframe, although z/OS programs may have to be modified to initiate interactions.

Figure 3-11 provides an overview of the Substation ES deployment. The substation itself runs on the z/OS mainframe and can initiate or provide access to both CICS and IMS programs. Off-mainframe communications can use either Enterprise Message Service or Rendezvous as a transport. Data in these communications is represented in mainframe format. Managing and monitoring Substation ES can be done from a browser-based UI.

The ActiveMatrix BusinessWorks Plug-in for Data Conversion provides convenient facilities for accessing data in this format. Similar facilities are provided in the Eclipse IDE provided with the product. These tools significantly reduce application development time.

# TIBCO Mainframe Service Tracker

The TIBCO Mainframe Service Tracker (Figure 3-11) is a z/OS subsystem that can monitor jobs and job steps as well as SYSLOG messages

![](bbox=[0.22, 0.78, 0.92, 0.94])

Figure 3-11: Substation ES Deployment Overview