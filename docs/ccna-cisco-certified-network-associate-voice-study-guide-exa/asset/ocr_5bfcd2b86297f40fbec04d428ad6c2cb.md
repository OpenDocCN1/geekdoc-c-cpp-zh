# ## SIP Features

SIP uses text-based communications. Stated differently, the ASCII character set is used to communicate SIP messages. Because of this format, SIP is easier to analyze and understand than most other networking protocols. Instead of worrying about the number of bits in a header that represent specific data, we are looking at plain text that clearly indicates the meaning. The messages are still said to have headers, but the headers are in ASCII text format instead of binary bit format.

SIP is a simplified protocol when compared with the H.323. This simplification comes from the fact that SIP includes everything needed to establish the VoIP call instead of using one protocol for call setup (H.225.0 in H.323 networks) and another for feature negotiation (H.245 in H.323 networks). Many assume this always makes SIP the better choice; however, it could be argued that H.323's componentized nature makes it more flexible for implementation. Regardless of the side of the argument you take, you must understand the basics of both protocols for the Cisco CVOICE and CCNA Voice exams.

When it comes to SIP addressing (locating SIP endpoints), the addresses may look very familiar to you. For example, an address for Tom Carpenter may look like this:

SIP://Tom.Carpenter@SysEdCo.com

This address format is technically known as a URI (Uniform Resource Identifier). URIs provide a standard way to reference a resource on an internetwork. Here are some other examples of URIs:

HTTP://www.SysEdCo.com
FTP://ftp.download.com

Do you recognize these? You probably do because they are used all over the Internet. URIs work for HTTP, FTP, SIP, and even Gopher (although Gopher is not as popular today as it once was). You can also access a SIP device securely by using the secure SIP protocol (which takes advantage of TLS) with a URI like the following:

SIPS://Tom.Carpenter@SysEdCo.com

As you can see, even the addressing used in the SIP world is based on Internet standards. The most important feature of the SIP protocol that has allowed it to catapult beyond its predecessors to success seems to be this use of existing Internet standards whenever possible.