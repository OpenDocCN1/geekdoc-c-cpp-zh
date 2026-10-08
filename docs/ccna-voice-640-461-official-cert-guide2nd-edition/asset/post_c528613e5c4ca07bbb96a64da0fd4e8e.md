
# Foundation Topics

## Understanding CUCM Mobility Features

CUCM incorporates a range of Mobility features that allow a user to interact with their Unified Communications devices and applications regardless of where he happens to be. The goal is to extend the ability to communicate with customers or colleagues using their enterprise IP phone number, both for inbound and outbound calls, in a seamless and flexible way. The following sections describes the features and configuration of some of the Mobility capabilities of CUCM.

## Describe Mobile Connect

Mobile Connect is often called Single Number Reach: A user's IP phone number becomes the single number by which all the various devices that person uses can be reached, including home phones, mobile phones, Internet-based VoIP numbers, and so on. The benefit is that a single point of voice contact is published for simplicity and consistency, whereas a range of devices can actually take calls, which provides maximum flexibility and reachability for the person almost regardless of where they may be or which communication method they may have available to them.

The user experience is simple, but powerful; if he receives a call at his business number, his IP phone rings. In addition, all the other devices configured for Mobile Connect ring at the same time. Whichever device is answers the extended call, and all other devices stop ringing.

Suppose the user answers the call on his mobile phone on the way to his office. When he gets to his desk, he has the option of picking up the call at his IP phone by pressing a softkey. The call is seamlessly transferred to the desk phone, and the caller may not even realize it has happened.

Likewise, the user can be in a call on his IP phone and redirects it to his mobile device as he leaves the office, without the other party knowing that it has happened (except, of course, the possibility of a change in background noise or voice quality on a cell phone).

If the user calls a colleague's IP phone by dialing his Direct Inland Dial (DID) from his mobile phone, CUCM recognizes the Automatic Number Identification (ANI) (the Caller ID) of the user as matching a Remote Destination Profile, which has a shared line with the user's directory number (DN). The call to the colleague's IP phone is presented as being from the DN of the user's IP phone. This functionality also allows the user to call in to the Cisco Unity Connection-messaging system and have Easy Message Access to his personal mailbox (which is associated with the DN on his IP phone).

Note: Most implementations of Mobile Connect use access codes for remote destinations. If this is the case, some digit manipulation of the incoming ANI may be necessary to match the entry Remote Destination Profile number pattern. Alternatively, the CallManager Service Parameter Matching Call ID with Remote Destination is set to Partial Match, which causes CUCM to make the closest match with a Remote Destination Profile, starting with the least-significant digit of the ANI.

## Unified Mobility Architecture

Mobile Connect uses Remote Destination Profiles to configure virtual phones that share several configuration settings with the user's primary IP phone. In effect, the Remote Destination Profiles act as phones with shared lines; when the primary number rings, but the system configuration redirects the call out to the PSTN to ring the other devices.

Remote Destination Profiles are configured with many of the same settings as the physical IP phone, including a Partition, Device Pool, Calling Search Space (CSS), User and Network Music on Hold (MoH), and, of course, the DN. The profile also includes a Rerouting Calling Search Space to allow the system to route calls to the device, even if that call would normally be restricted by the CSS of the IP phone.

Up to ten Remote Destination Profiles can be defined per user. Immediate complexities emerge with the behavior of the Mobile Connect feature: How long should the system wait before ringing the Remote Destination Profile phones? How long should the remote devices be to ring? How long must the remote device ring before the call can be picked up on it? The adjustment of these timers can greatly improve the utility of the Mobile Connect feature, as well as avoiding unwanted behavior, such as calls going to voicemail too soon or possibly going to some other voicemail (such as the personal voicemail at the user's home phone).

## Access Lists

Not to be confused with IOS router access control lists, these Access Lists give both administrators and users control over which calls will ring which Remote Destination Profile devices, and at what time of day.

Access lists filter calls based on the Caller ID; they can be configured to allow certain number patterns (called a white list) or to block certain number patterns (called a black list). The callers are identified using three types of:

- **Not available:** The Caller ID is not provided.
- **Private:** The Caller ID is not displayed.
- **Directory number:** The Caller ID matches a specific number, or a wildcard-defined range of numbers (using the digits 0 through 9, *, #, and the wildcards of X and !).

## Time-of-Day Access

Each Remote Destination Profile can be configured with a schedule that controls when should be included in the set of remote device that will ring. By default, all remote devices ring. The time zone of the actual remote device should be specified so that the time-of-day rules apply correctly.

For incoming calls, the Time-Of-Day rules are processed first. If the time-of-day rule allows the call to be extended to the Remote Destination Profile, any configured Access Lists are processed next. If the Access List allows the call, it is extended to the Remote Destination device.

**Key Point:** Avoid using empty Access Lists. An empty Access List selected in a white list causes no calls to be routed; an empty Access List in a black list causes all calls to be routed to the remote destination device.

## Mobile Voice Access

Mobile Voice Access (MVA) provides the same single-number consistency and flexibility for outbound calls from mobile: By accessing the CUCM system from their mobile device, they can instruct the primary to place calls and have the call appear from their IP phone using their primary IP phone number (assumed to be a DID, but could be the business number). As a result, their physical location has no impact on voice communication consistency. Whether they are sitting in front of their IP phone or using their mobile phone from the golf course, the calls they all appear to come from their primary business number.

To use the feature, the user dials in a specific PSTN DID to access the MVA service. A specially configured XML gateway routes calls to an Interactive Voice Response (IVR) application that guides the user through his MVA session. The IVR app provides security by prompting the user to authenticate with their User ID (optional) and PIN. Once successfully authenticated, the IVR prompts the user for the number they want to dial. The user enters the PSTN number and the system places the call, using the ANI of the user's IP phone. The user can switch between his mobile device and his IP phone during the call. The called party sees the Caller ID as that of the IP phone, providing the single-number consistency and recognition, as well as ease of callback from a call. Figure 12-1 shows the basic flow.

![](img/e47862dc47b4e5de0cde3b4550ad65_357_0.png)

# Implementing Mobility Features in CUCM

The configuration of the various Mobility features in CUCM is not difficult, but it is repetitive and potentially time-consuming, especially when many users need to be. This section outlines the configuration tasks for the Mobility features described earlier.

## Configuring Mobile Connect

Many different components interact to allow Mobile Connect to function. The basic steps to configure Mobile Connect are as follows:

1. Configure Softkey Templates to include the Mobility key.
2. Configure user accounts for Mobility.
3. Configure IP phones to support Mobility features.
4. Create Remote Destination Profiles and assign them to each user.
5. Add Remote Destinations to Remote Destination Profiles.
6. Configure ring schedules for each Remote Destination.
7. Configure Access Lists.
8. Apply Access Lists to Remote Destinations.
9. Configure Service Parameters.

Each of the following steps describes these configuration steps in detail.

### Step 1: Configure Softkey Templates

To use Mobile Connect, the user activates a softkey on his IP phone. Complete the following tasks to add the softkey to use this feature:

1. Navigate to Device > Device Settings > Softkey Template.
2. Select, copy, and modify or a new template.
3. In the Related Tasks pull-down, select Softkey Layout and click Go.
4. Add the Mobility softkey to the OnHook and Connected call states lists. Save after each move.

Figure 12-2 shows the Softkey Template with the Mobility key added.

### Step 2: Configure User Accounts for Mobility

Individual user accounts must be enabled for Mobility, and some settings tuned for optimal functionality. Complete the following steps to set up the user accounts for Mobility:

1. Navigate to User Management > End User and select a user.
2. Check the Enable Mobility checkbox.
3. Set the Remote Destination Limit (maximum 10).
4. Set the Maximum Wait Time for Desk Pickup timer. This is how much time (milliseconds) is allowed for the user to pick up a call that was redirected from the remote device to the IP phone. The default is 10,000 ms (10 sec) with a maximum of 30,000 ms (30 sec).

![](img/e47862dc47b4e5de0cde3b4550ad65_358_0.png)
