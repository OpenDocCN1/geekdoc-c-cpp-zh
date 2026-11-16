
Why take this approach, you might ask? If you consider the fact that most customers' biggest reservation about adopting cloud-based solutions is security, then it makes sense for SAP to remove as many potential security risks from the mix as possible. Using a federated approach to authentication reduces the threat of sensitive user information being compromised in the cloud. Plus, it also offers the added benefit of letting customers leverage preexisting IdP solutions they might have in-house.

In this section, you'll learn how to configure and leverage federated authentication using the industry-standard Security Assertion Markup Language (SAML) 2.0 protocol. This protocol is the primary protocol used by SAP HCP for the purposes of authentication and single sign-on (SSO).

### 8.5.1 SAML Overview

Before you begin looking at how to configure SAML-based authentication scenarios, it's helpful to understand a little more about what SAML is (and isn't). As its name implies, SAML defines an XML-based vocabulary that's used to exchange authentication and authorization data between parties. Within the vernacular, the negotiating parties are referred to as the identity provider (IdP) and service provider, respectively.

In addition to the XML-based messages it defines, the SAML 2.0 standard also specifies a series of protocols that describe how messages are exchanged between users, the IdP, and the service provider. The typical message flow for a SAML authentication request processed through SAP HCP is illustrated in Figure 8.12.

Within the flow diagram contained in Figure 8.12, you can observe the following:

- 1 The process begins with a user attempting to access a secure web application hosted on the service provider. As you can see in Figure 8.12, SAP HCP plays the role of service provider in this scenario.
- 2 Upon receipt of the request, the SAP HCP server determines via declarative constraints defined in the application's web.xml file that the user needs to authenticate before the server can decide whether or not the user is authorized to access the application. Assuming that the authentication method is set to FORM (refer back to Section 8.3.1), the request will be handed off to a JAAS-based login module. This module will generate a SAML authentication request (i.e., a SAML AuthnRequest message) and send it back to the user in an HTTP 302 redirect message.
- 3 The browser then follows the redirect and forwards the SAML authentication request on to the SSO login page defined by the IdP. By default, this results in the user being routed to the login page of the SAP ID Service, as shown in Figure 8.3. Naturally, the look and feel of the page would be different if an alternative IdP is being used instead.
- 4 Once the user fills in his or her user credentials and submits the login form, the login request is forwarded on to the IdP.
- 5 Upon receipt of the login request, the IdP will process the request and return a SAML response message back to the user's browser.
- 6 From here, the SAML response is forwarded on to the service provider, where it's unpacked to determine if the user was authenticated. Assuming the authentication is successful, then the web container will grant access to the target web application.

![](img/cf7012644082c115a2181376d9b7486d_350_0.png)

Figure 8.12 Tracing a Typical SAML Authentication Flow within SAP HCP

For the most part, developers don't really have to concern themselves with the intricacies of the authorization flow illustrated in Figure 8.12, because these details are handled automatically by the JAAS login module(s) of SAP HCP. With that being said, though, we should point out that a SAML response message contains more than just a flag indicating whether or not a user is authorized. The response message also contains a series of assertions (hence the name), which contain user attributes (e.g., first and last name, email address, telephone number, etc.), and sometimes authorization decision statements, which can be used to determine user authorizations. We'll explore some of the ways these attributes are used in Section 8.5.3.

### 8.5.2 Configuring Trusted Identity Providers

As we noted earlier, SAP HCP is configured by default to utilize the SAP ID Service as its trusted IdP. This SAP ID Service is the same one users use to access SCN and other SAP-related sites. Although this default IdP is suitable to get things up and running, most customers will prefer to connect with a preexisting IdP they already have in-house (e.g., Microsoft Active Directory Services). This IdP could be provided by a third party on the Internet or on-premise; it doesn't really matter one way or another to SAP HCP.

In order to leverage another IdP from within SAP HCP, you must configure a trust relationship between SAP HCP (which plays the role of a service provider) and the target IdP. To demonstrate how this works, let's take a look at how you can configure a trust relationship to the simplified (but fully SAML-compliant) IdP bundled with the local runtime environment included in the SAP HCP SDK. The configuration steps are as follows:

- 1. Open the SAP HCP Cockpit and access the Trust tab. This will open the TRUST MANAGEMENT page shown in Figure 8.13. To create a new trust relationship, choose the Custom configuration type in the CONFIGURATION TYPE dropdown list.

![](img/cf7012644082c115a2181376d9b7486d_352_0.png)

Figure 8.13 Configuring Access to a Local Identity Provider: Part 1

- 2. As soon as you select the custom configuration type, the screen will refresh itself to display details about the SAP HCP service provider (e.g., the provider name, its signing key and certificate, and so on). Although you have the option of overriding default values here, for now simply accept the defaults and click on the Get Metadata hyperlink (highlighted in Figure 8.14). This action will trigger the download of an XML file containing metadata about the service provider. (This metadata is encoded in an EntityDescriptor message, as defined by the SAML 2.0 standard.) For now, simply save the file locally so that you can use it a little bit later on.

- 3. On the IdP end of the exchange, you need to generate a metadata file containing information about the IdP. To perform this step, start up your local SAP HCP runtime and open a browser window to http://localhost_hcp_instance_host}:{port}/saml2/localidp/metadata, as shown in Figure 8.15. Once again, you need to save the generated XML file so that you can import it in a later step.

![](img/cf7012644082c115a2181376d9b7486d_353_0.png)

Figure 8.14: Configuring Access to a Local Identity Provider: Part 2

![](img/cf7012644082c115a2181376d9b7486d_353_1.png)

Figure 8.15: Configuring Access to a Local Identity Provider: Part 3

- 4. With the IdP metadata in hand, you can go back to the SAP HCP Cockpit and navigate to the TRUSTED IDENTITY PROVIDER subtab (Figure 8.16). Here, click on the Add TRUSTED IDENTITY PROVIDER link to create the new trusted IdP configuration.

![](img/cf7012644082c115a2181376d9b7486d_354_0.png)

Figure 8.16 Configuring Access to a Local Identity Provider: Part 4

- 5. Figure 8.17 shows the popup box that opens whenever you go to create a new trusted IdP. Although there are a lot of attributes that have to be filled in to define a trust relationship, the good news is that you don't have to key in the attributes by hand. Instead, you can copy this information from the metadata file created in step 3 by clicking on the BROWSE... button adjacent to the META-DATA FILE field and selecting the XML file generated by the local IdP. Once the attributes are copied over, you can save the trusted IdP configuration by clicking on the SAVE & Close button.

- 6. The last step is to open the server configuration on the local IdP to plug in the metadata file generated by the SAP HCP service provider. This can be achieved by copying and pasting the XML file created in step 2 into the CONFIG_MASTER/com.sap.core.j2ee.security.saml2.cfg/LOCALIDP folder, as shown in Figure 8.18.
