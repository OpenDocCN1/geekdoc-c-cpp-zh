![](bbox=[0.138, 0.092, 0.805, 0.385])

**Figure 27-18**  *Connecting Branches Directly to the Internet for Public Cloud Traffic*

However, when the per-branch Internet connections are added for the first time, the new Internet links create security concerns. One of the reasons an enterprise might use only a few Internet links, located at a central site, is to focus the security efforts at those links. Using an Internet connection at each branch changes that approach. But many enterprises not only use the Internet at each site, but rely on it as their only WAN connection, as shown with Internet VPNs back in Chapter 15.

# ## Virtual Network Functions and Services

This third and final major section of the chapter now looks more closely at what happens with networking functions inside the public cloud environment. In particular, this section introduces the concept of a virtual network function (VNF), by showing how a public cloud installation could implement routers and firewalls as VMs. The remainder of this section looks at options for changing how DNS, DHCP, and NTP could work when migrating an application from inside an enterprise to being hosted in a public cloud service.

# ### Virtual Network Functions: Firewalls and Routers

When you start to peel back the layers of what you get in a public cloud service, you can begin to see familiar functions and features. Public cloud providers may not use all the same old terminology for traditional approaches to IT, but to anyone who has worked in IT, many of the ideas should look familiar.

As an example, take the following basic scenario in which an enterprise orders an IaaS service from a public cloud provider:

+   - The consumer wants a number of IaaS servers.
+   - All VMs will run the same app; the consumer wants multiple VMs to deal with server load.