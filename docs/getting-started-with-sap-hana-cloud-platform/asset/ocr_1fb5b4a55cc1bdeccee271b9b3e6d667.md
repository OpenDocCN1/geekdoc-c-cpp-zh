+   1. Due to the presence of the mediating authorization server, a client application never gets its hands on the user's account credentials.

+   2. OAuth access tokens are designed to provide a client with the minimum amount of access it needs to do its job. Therefore, if a client is granted an access token to view basic information, it can't use this token to view other hidden data, modify data, and so on.

+   3. Normally, OAuth access tokens have an expiration date, which ensures that they don't become a long-term security risk.

+   4. OAuth access tokens can be revoked at any time to block access from particular clients and so on. This revocation process can be performed without disturbing the resource owner's account (e.g., by forcing the user to change his or her password).

Collectively, these principles lead to a very secure authorization protocol that offers the flexibility and convenience required by many modern application clients.

# 8.6.2 Understanding the OAuth Authorization Flow

Now that we've reviewed the basic concepts surrounding OAuth, let's narrow our focus a bit and consider how OAuth fits into the SAP HCP development landscape. Looking at the flow diagram in Figure 8.28, you can identify the positioning of OAuth-related components as they relate to SAP HCP. Here, you can observe the following:

+   - SAP HCP comes equipped with its own OAuth authorization server that can be used to process token requests and so on.

+   - SAP HCP also assumes the role of resource server, playing host to a number of web resources and APIs that you might want to provide with delegated access via OAuth. The SAP HCP Servlet/web container offers excellent support for OAuth-based security configurations.

+   - The SAP HCP authorization server components are able to delegate user authentication requests to any of the trusted SAML-based IdPs that might be configured within the landscape.