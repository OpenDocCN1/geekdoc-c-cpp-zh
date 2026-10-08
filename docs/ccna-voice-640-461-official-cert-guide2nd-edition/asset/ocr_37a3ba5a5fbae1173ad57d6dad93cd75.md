# Foundation Topics

# Understanding CUCM Mobility Features

CUCM incorporates a range of Mobility features that allow a user to interact with their Unified Communications devices and applications regardless of where he happens to be. The goal is to extend the ability to communicate with customers or colleagues using their enterprise IP phone number, both for inbound and outbound calls, in a seamless and flexible way. The following sections describes the features and configuration of some of the Mobility capabilities of CUCM.

# Describe Mobile Connect

Mobile Connect is often called Single Number Reach: A user's IP phone number becomes the single number by which all the various devices that person uses can be reached, including home phones, mobile phones, Internet-based VoIP numbers, and so on. The benefit is that a single point of voice contact is published for simplicity and consistency, whereas a range of devices can actually take calls, which provides maximum flexibility and reachability for the person almost regardless of where they may be or which communication method they may have available to them.

The user experience is simple, but powerful; if he receives a call at his business number, his IP phone rings. In addition, all the other devices configured for Mobile Connect ring at the same time. Whichever device is answers the extended call, and all other devices stop ringing.

Suppose the user answers the call on his mobile phone on the way to his office. When he gets to his desk, he has the option of picking up the call at his IP phone by pressing a softkey. The call is seamlessly transferred to the desk phone, and the caller may not even realize it has happened.

Likewise, the user can be in a call on his IP phone and redirects it to his mobile device as he leaves the office, without the other party knowing that it has happened (except, of course, the possibility of a change in background noise or voice quality on a cell phone).

If the user calls a colleague's IP phone by dialing his Direct Inland Dial (DID) from his mobile phone, CUCM recognizes the Automatic Number Identification (ANI) (the Caller ID) of the user as matching a Remote Destination Profile, which has a shared line with the user's directory number (DN). The call to the colleague's IP phone is presented as being from the DN of the user's IP phone. This functionality also allows the user to call in to the Cisco Unity Connection-messaging system and have Easy Message Access to his personal mailbox (which is associated with the DN on his IP phone).

Note: Most implementations of Mobile Connect use access codes for remote destinations. If this is the case, some digit manipulation of the incoming ANI may be necessary to match the entry Remote Destination Profile number pattern. Alternatively, the CallManager Service Parameter Matching Call ID with Remote Destination is set to