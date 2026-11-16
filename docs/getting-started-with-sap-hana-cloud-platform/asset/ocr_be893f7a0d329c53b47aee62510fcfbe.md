# 6.4.2 Working with the OpenCMIS API

In order to understand how to tap into the functionality of the Document Service, it's helpful to take a look at how you can interact with it using the OpenCMIS API. Therefore, in this section, we'll show you how this API can be used to connect to a repository, add and remove content, and search for content after the fact. Once you grasp these concepts, it will be much easier to see how to exploit some of the value-add features of the Document Service within your application scenarios.

To guide this discussion, we would recommend that you open the AttachmentProcessorBean.java file contained within this chapter's source code bundle in the com.sappress.hcbook.chp06.document package (downloadable from www.sap-press.com/3638). This session EJB is used within the incident management application to process attachments that are uploaded for particular incidents (see Figure 6.44). As such, it provides a fairly typical example of how the Document Service is used from an application perspective.

![](bbox=[0.153, 0.426, 0.547, 0.613])

# Establishing a CMIS Session

Before you can begin doing anything useful with the Document Service, you first need to establish a CMIS session. This session essentially connects you with the application-specific content repository that you wish to interact with.

The code excerpt contained in Listing 6.20 demonstrates how you can create a CMIS session using the OpenCMIS library. The code begins by looking up the core com.sap.ecm.api.EcmService service façade provided by the Document Service via the JNDI context. Although this service is managed by the Document Service, you do have to create a resource reference to it in the application's web.xml file.