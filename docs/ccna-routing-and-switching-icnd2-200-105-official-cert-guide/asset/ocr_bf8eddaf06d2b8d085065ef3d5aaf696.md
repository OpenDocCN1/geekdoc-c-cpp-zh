# Chapter 20

To allow the hosts to remain unchanged, the routers have to do some more work, as defined by one of the FHRP protocols. Generically, each FHRP makes the following happen:

+   1. All hosts act like they always have, with one default router setting that never has to change.
+   2. The default routers share a virtual IP address in the subnet, defined by the FHRP.
+   3. Hosts use the FHRP virtual IP address as their default router address.
+   4. The routers exchange FHRP protocol messages, so that both agree as to which router does what work at any point in time.
+   5. When a router fails, or has some other problem, the routers use the FHRP to choose which router takes over responsibilities from the failed router.