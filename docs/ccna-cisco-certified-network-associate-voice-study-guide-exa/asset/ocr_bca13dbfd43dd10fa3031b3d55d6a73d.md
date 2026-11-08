![](bbox=[0.055, 0.118, 0.955, 0.195])

Figure 16-2 illustrates the topology of fax and modem pass-through. The difference between Figure 16-1 and 16-2 should be clear. Fax and modem relay uses UDP across IP and consumes little overhead above that required to send the actual fax data. Fax and modem relay is a much more efficient solution than fax and modem pass-through.

# ### Store and Forward

Store and forward is a fax-only solution, but it is the most interesting of the three. With store and forward, the fax comes into the router, and the router terminates the fax communications. In other words, the router is the fax machine, and it converts the fax into an e-mail message with an attached TIF image file. The e-mail is sent to the configured destination. Additionally, internal users can e-mail a TIF file to the router (voice gateway), and the router can send the TIF file as a fax message to a remote fax machine. Figure 16-3 illustrates this concept.

In the Cisco world, two types of store and forward faxing are available. On-ramp faxing occurs when a fax comes in from the PSTN or external voice network. With on-ramp faxing the voice gateway converts an incoming fax to an e-mail. Off-ramp faxing occurs when an e-mail comes into the voice gateway and is converted to a fax for transmission. With off-ramp faxing the voice gateway converts an incoming e-mail to an outgoing fax communication.

> > **Exam Watch**
> >
> > Configuring store and forward faxing is much more complicated than fax and modem relay or fax and modem pass-through. You will not be required to know more about store and forward faxing than its basic functionality for the CVOICE exam.

![](bbox=[0.055, 0.805, 0.95, 0.915])