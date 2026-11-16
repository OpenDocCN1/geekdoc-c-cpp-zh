After the OAuth client is configured, you need to plug the generated client ID into the client application's web.xml file so that it can include the client_id attribute in authorization requests at runtime. From here, you can deploy the application and fire it up on your local SAP HCP runtime. As you can see in Figure 8.33, right off the bat you'll be prompted to authenticate and then authorize the client to look up flight information via the sample API created in the EXAMPLE08_02 application that's deployed on the cloud-based SAP HCP instance. Although this scenario's a bit contrived in that you're playing both the resource owner role and the resource provider role, it's not hard to imagine this authorization handshake playing out between, say, a mobile client and a web API that you've deployed on SAP HCP.

![](bbox=[0.146, 0.353, 0.856, 0.683])

Figure 8.33 Authorizing the Sample Client to Look Up Flight Information

As soon as the client is authorized, the application redirects to the FLIGHT SEARCH page shown in Figure 8.34. From this page, you can submit various queries to the flight search API by filling in selection parameters and clicking on the Go button.

On the server side, you can manage the OAuth access tokens that are allocated by the authorization server by opening the SAP HCP Cockpit and clicking on the AUTHORIZATIONS tab. From the Token subtab shown in Figure 8.35, you can view the access tokens that have been allocated and revoke them as necessary.