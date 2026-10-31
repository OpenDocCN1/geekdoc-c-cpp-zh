![](bbox=[0.24, 0.14, 0.84, 0.58])

Figure 3-13: TIBCO Adapter for IBM i Deployment

# Mainframe and iSeries File Adapters

The TIBCO Adapter for Files z/OS (MVS) and TIBCO Adapter for Files (IBM i) provide off-mainframe access to files on their respective platforms. Files are accessible either in their entirety by block transfer (whole file) or by record for record-based processing.

Capabilities on the two platforms are slightly different. On the z/OS platform, applications can write to VSAM, sequential datasets (SEQs), generation dataset groups (GDGs), and partitioned datasets (PDSs). Applications can trigger the publishing of these same file types by sending a message. The adapter can also be configured to poll partitioned datasets (PDSs) and publish the files when they change. For the iSeries platform, the adapter can write and publish sequential (SEQ) files.

Deployment of both adapters is similar (Figure 3-14). The adapter itself resides on the mainframe, providing services via the TIBCO adapter protocol using either the Enterprise Message Service or Rendezvous transports. The TIBCO adapter protocol is supported by a wide range of products including ActiveMatrix Service Grid, ActiveMatrix Service Bus, and ActiveMatrix BusinessWorks.