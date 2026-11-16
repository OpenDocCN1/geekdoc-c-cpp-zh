+   - If you'd like to perform OData API calls on behalf of the currently logged in user, then set the AUTHENTICATION field to OAuth2SAMLBEARER ASSERTION. This will open a number of additional fields. Alternatively, you could configure basic authentication here. Keep in mind that basic authentication is acceptable for testing, but is not recommended for production accounts.
+   - For AUDIENCE, enter “www.successfactors.com”.
+   - Set the CLIENT KEY to the same value you obtained from the SuccessFactors API Key field in the OAuth 2.0 Client Application view, visible in Figure 11.14.
+   - Fill the TOKEN SERVICE URL with the corresponding SuccessFactors landscape-specific URL.
+   - Configure NAMEQUALIFIER to “www.successfactors.com”, similarly to the AUDIENCE field.
+   - For the OAuth flow with SuccessFactors, the companyID field must be filled with the corresponding company ID.
+   - Last but not least, set the same value you’ve pasted in to CLIENT KEY for ASSERTIONISSUER.
+   - Click on SAVE, and you’re done.

If you need to create more of the OData destinations, then simply repeat the steps above accordingly, starting with the OAuth client creation in the SuccessFactors OneAdmin tool.

![](bbox=[0.05, 0.6, 0.85, 0.85])

Figure 11-15. Creating a SuccessFactors OData API Destination in the SAP HCP Extension Account