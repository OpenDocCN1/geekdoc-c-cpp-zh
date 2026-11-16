Once these configuration steps are in place, the changes will take effect immediately. To the end user, all of this will be transparent, save for the fact that the logon page will look a little bit different (see Figure 8.19).

![](bbox=[0.14, 0.185, 0.86, 0.445])

Figure 8.19 Accessing the SSO Logon Page of the SAP HCP Local Runtime

For the most part, the configuration steps required to establish a trust relationship with another SAML-compliant IdP are largely the same as the ones used to connect with the local test IdP. The primary differences lie in how you generate the IdP metadata and how you configure the trust relationship to the service provider from within the IdP itself. Fortunately, there are how-to guides available on SCN that describe IdP-specific requirements.

Before we move on, we should point out that it's technically possible to configure and run multiple IdPs simultaneously. In this scenario, you have a default IdP (of your choosing) and one or more alternative IdPs. At runtime, authentication requests will continue to be routed through the default IdP as usual. However, you can force authentication through one of the alternate IdPs by adding the query string parameter `saml2idp=<idp_name>` to the end of the application URL.

# 8.5.3 Implementing Assertion-Based Group Mapping

In Section 8.3.3, we observed just how tedious it can be to assign roles or groups to users—especially whenever you have lots of users to maintain. Fortunately,