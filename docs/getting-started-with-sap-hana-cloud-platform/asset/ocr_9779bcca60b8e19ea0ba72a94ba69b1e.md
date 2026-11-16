4. Assuming the user grants the request, control picks up on the SAP HCP authorization server, which generates an authorization code and invokes the OAuth callback URL provided in the original authorization request.

5. The OAuth callback service on the client application will receive the authorization code and invoke the token endpoint of the SAP HCP authorization server to exchange the authorization code for an access token.

6. After the access token is received, the client application will redirect the user's browser to the application start page where users can begin searching for flights.

7. Finally, whenever the user submits a flight query, the client will format the REST call and embed the access token in the HTTP request headers. If all goes well, then the flight API will respond with the desired flights, and the results will be parsed by the client application and displayed in the results list.

Looking closely at Figure 8.31, you can see that the client application interfaces with a couple of endpoints on the SAP HCP authorization server in order to obtain an OAuth access token. This raises the question: How do you know which URLs to hit when developing a client application? As is the case with most SAP HCP-related configuration items, you must go to the SAP HCP Cockpit to find out this information. From the main landing page, you can find the OAuth URLs by opening the OAuth tab, as shown in Figure 8.31.

![](bbox=[0.05, 0.56, 0.85, 0.84])

Figure 8.31 Accessing OAuth Authorization Server Endpoints