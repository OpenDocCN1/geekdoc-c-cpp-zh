As of the time of writing, the OpenSocial specification has recently been incorporated into the W3C Social Web Working Group. As per the group's charter, this move is intended to help extend the reach of OpenSocial in the enterprise and also expand its scope. Over time, it's likely that we'll see these innovations find their way into SAP HANA Cloud Portal.

The block diagram in Figure 9.4 provides a closer look at how the OpenSocial framework is integrated into the SAP HANA Cloud Portal architecture. Here, in addition to the core Apache Shindig container, you can see that SAP HANA Cloud Portal also defines supplemental services that proxy requests from widgets to server-side resources (such as RESTful services), aid in the rendering of gadgets, and so forth. The gadget components are provided via one or more gadget providers. Much of the time, the only gadget provider in play is SAP HCP itself, but it's possible to integrate gadgets deployed on other SAP HCP accounts and even from an external server; it doesn't really matter one way or another to SAP HANA Cloud Portal.

![](bbox=[0.05, 0.45, 0.85, 0.7])

Figure 9.4 Content Flow for SAP HANA Cloud Portal

As we wrap up this architecture section, we recognize that you may have many questions about how all the various pieces of SAP HANA Cloud Portal's OpenSocial implementation fit together. Indeed, because many SAP developers may be encountering OpenSocial for the first time, there's a lot to wrap your head around early on. As we progress through this chapter and you have a chance to create a