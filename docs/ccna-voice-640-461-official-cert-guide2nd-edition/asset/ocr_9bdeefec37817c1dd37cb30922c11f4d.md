# Foundation Topics

# Configuring Physical Voice Port Characteristics

Before you can dive fully into the configuration of dial-plans using dial peers, you must first think about the physical characteristics of the voice ports on the router. Obviously, the voice ports plug into cables, which eventually connect to far-end devices. Beyond that, you can tune a few additional settings on the router to allow the voice ports to operate exactly to your specification. This section divides the discussion of these configurations into analog and digital forms.

# Configuring Analog Voice Ports

Unlike Ethernet, when you connect a cable to an analog voice port on a router, it just works (provided a signal is coming from the other end). The router receives the electrical signals from the line and processes them normally. In addition to normal call processing, each interface type has a few settings you can tune to change the way it operates with the other end of the connection. This section describes configuration options for Foreign Exchange Station (FXS) ports and Foreign Exchange Office (FXO) ports.

# Foreign Exchange Station Ports

FXS ports connect to end stations—that is, typical analog devices such as telephones, fax machines, and modems (shown in Figure 6-1).

> Key Topic

![](bbox=[0.131, 0.631, 0.515, 0.843])

Figure 6-1 FXS Port Connections

When you are ready to configure your FXS voice ports, the best place to start is to find out what voice ports your router is equipped with. You can do this quickly by using the show voice port summary command, as shown in Example 6-1.