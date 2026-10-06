the use of arguments.
Include the option to use compression tools such as tar and/or gzip so that we don't need to send as much data over the network.
Consider rewriting the script in a more flexible language such as Perl or Ruby so that we can do more with the information that Netcat is sending or receiving.
Take in the listening and/or sending ports as an argument so that we are more flexible.
Add error handling. In the present state of our scripts, it doesn't take much to get us off the rails, and we won't handle issues gracefully.
Add progress monitoring. We can use a tool as pv4 to monitor the progress of our file transfer from either or both ends. These are only the updates that immediately present themselves, and there are sure to be quite a few others we come up with a little thought. Although we could access this functionality by using ready-made tools, such as Secure Shell (SSH), to provide this functionality, it is often a good thing when we can improvise what we need out of the materials we might have at hand.

# Nmap

As we discussed earlier in the chapter, we can make use of NSE to extend the capabilities of Nmap. In this section we will discuss the Lua programming language, in which NSE scripts are written, as well as some specific examples of what we can do with Nmap.

# Working With Service Probes in Nmap

One of the handy things we can do with Nmap is to probe for services on our target hosts. This allows us to add custom service definitions to Nmap, so we can detect running services outside the default list, specified in the nmap-service file, which is located in /usr/share/nmap on Kali. The nmap-service file is used to perform a simple match against the port number, and provides us with the name of the service that typically runs on that port. When we run a default Nmap scan