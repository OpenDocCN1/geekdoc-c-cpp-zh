# INSIDE THE EXAM

# Why Is TCP/IP Important?

TCP/IP is the foundational protocol of the Internet. Modern private networks primarily use this protocol as well. If you do not know the basics of IP, TCP, and other protocols in this suite, you will not be able to administer a modern network.

The success of TCP/IP has been largely due to its utilization on the Internet. If you wanted to browse web pages, download from FTP sites, or read text at gopher sites, you had to be running the TCP/IP protocol. Many early networks ran TCP/IP as well as some other protocol like IPX/SPX (Internetwork Packet Exchange/Sequenced Packet Exchange) or Banyan Vines. First, network vendors began by supporting TCP/IP alongside their proprietary protocols, and eventually they moved their systems not only to support the TCP/IP suite, but also to rely upon it. Today, Novell, Microsoft, Unix,

Linux, and Apple computers all use TCP/IP as the primary communication protocol.

A very gradual transition is happening in relation to the IP protocol. IPv6 has been available for a number of years, and operating systems have slowly incorporated it into their available protocols. Windows Vista has integral support of IPv6 as does Windows Server 2008. Unix and Linux machines have supported it for some time, and Apple's Mac OS X also supports it. Once IPv6 support is available on the vast majority of computers, we'll likely see it used more and more on our networks; however, the CCNA Voice exams will not test your knowledge of this protocol, according to the stated objectives as of late 2010.

Oh, and TCP/IP is the foundation for all VoIP communications. Of course, that's what this book and the CCNA Voice exams are all about.

The *Real-time Transport Protocol (RTP)* is a protocol designed for moving audio and video data on internetworks running IP. Unlike TCP, RTP is focused not on reliability but rather on rapid transfer. It is used when the data being transferred must arrive in a timely fashion or it provides little value. For example, an e-mail message can take two or three minutes to arrive, and once it has arrived you can read it just fine; however, a five-second statement made into a VoIP phone cannot take two or three minutes to arrive. That five-second statement would have been broken into many packets, and they must arrive very quickly. If there are large gaps in their arrival, either the call will be lost, or the listener will not be able to intelligently hear the message. RTP runs over UDP, which is discussed in a later section.