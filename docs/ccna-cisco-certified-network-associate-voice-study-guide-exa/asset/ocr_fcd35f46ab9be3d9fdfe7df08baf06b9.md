> > What, exactly, is the internet? Basically it is a global network exchanging digitized data in such a way that any computer, anywhere, that is equipped with a device called a “modem,” can make a noise like a duck choking on a kazoo.
> >
> > —Comedian Dave Barry

Modems were among the first devices that allowed for long-distance communications using computers. Fax machines allowed you to send pictures and text over the phone lines to anyone else having a fax machine. In their day, fax machines were amazing technological advances. Today, we are mostly stuck using these archaic solutions because so many business processes came to depend on them, and business processes are hard to change. E-mailing a scanned page or picture is a far superior solution to faxing. Wireless network connections to the Internet or the corporate network are many times faster than dial-up. However, the old technology still remains, and we must support it—even if it does sound like a “duck choking on a kazoo.”

This chapter helps you understand how you can support analog communication technologies in modern VoIP implementations. These analog methods (modems and fax machines) use sound to send information. Because of this technology selection, we must find a way to get the sound through the VoIP network without losing characteristics that define the information in the analog signal. This is where fax and modem pass-through and relay play a big role. In this chapter, you’ll first learn about the problems involved in supporting fax and modem communications on VoIP networks, and then you’ll learn about the solutions.

# CERTIFICATION OBJECTIVE 16.0.1

# 642-436: Implement Fax and Modem Support on a Gateway

Many business processes still depend on fax support and some depend on modems. Modems are used less often these days, but their use still lingers on for remote area connections. The Cisco Voice (CVOICE) exam 642-436 requires that you