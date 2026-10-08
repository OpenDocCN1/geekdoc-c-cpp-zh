
- Privacy setting
- Service subscriptions
- Dialing name

A Default Device Profile exists to allow users without a user Device Profile for a particular IP Phone type to log in using EM.

## Enable EM in CUCM

Enabling EM involves several steps, a few of which may need to be repeated many times depending on the number of phones and users in the system. The basic steps are as follows:

1. Activate the Cisco EM Service.
2. Configure EM service parameters.
3. Add the EM service.
4. Create a default Device Profile for each model of phone in use.
5. Create Device Profiles and subscribe them to the EM service.
6. Create end users and associate them with Device Profiles.
7. Enable EM for phones and subscribe phones to the EM service.

The steps are described in more detail in the following sections.

### Step 1: Activate the EM Service

- 1.1 In the Serviceability web page, navigate to Tools > Service Activation.
- 1.2 Select Cisco Extension Mobility, and then click Save.

### Step 2: Configure EM Service Parameters

- 2.1 In the CM Administration web page, navigate to System > Service Parameters. Select the server(s) you want to configure from the Server drop-down, and then select the Cisco Extension Mobility Service from the Service drop-down.

- 2.2 Scroll down to the Clusterwide Parameters section. Here, you can select whether to force EM login after a maximum login time has expired, and how long that timer is. This is also where you set the behavior for multiple logins (Multiple Logins Not Allowed, Multiple Logins Allowed, or Auto Logout), as described earlier. Additional settings here include enabling Alphanumeric User IDs (or using numeric only), choosing to remember and display on Alphanumeric (or not) the last User ID logged in the phone, and whether or not to clear the call lists for the last logged in user on logout.

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_322_0.png)

### Step 3: Add the EM Service

- 3.1 Navigate to Device > Device Settings > Phone Services.
- 3.2 Click New.
- 3.3 Give the EM service a name and description, if desired.
- 3.4 Type (or copy and paste from an external source) the following URL to the Service URL field:
http://IP_address_of_Publisher:8080/emapp/EMAppContext?device=#DEVICENAME#.
- 3.5 You may choose to add the Secure Service URL as well; if both are configured, and the IP Phone supports HTTPS, the secure URL will be used preferentially.
- 3.6 Make sure the Enable checkbox is selected.
- 3.7 You may choose to select the Enterprise Subscription checkbox as well. Doing automatically subscribes all IP Phones that support service subscription to the EM service; the administrator does not need to add the service manually to each device.

Figure 11-1 shows the Services Configuration page.

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_323_0.png)

Figure 11-1 Extension Mobility Service Configuration

### Step 4: Create Default Device Profiles

- 4.1 In the CM Administration web pages, navigate to Device > Device Settings > Default Device Profile.
- 4.2 Click Add New.
- 4.3 Select the Product Type (the phone model) and Device Protocol.

The available settings depend on the phone model and protocol chosen. You may select the Phone Button and Soft Templates, but you are not able to configure DNs or other specific phone button settings. Figure 11-2 shows the Default Device Profile page.

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_324_0.png)

Figure 11-2 Default Device Profile Configuration

### Step 5a: Create Device Profiles

- 5.1 Navigate to Device > Device Settings > Device Profile.
- 5.2 Click Add New.
- 5.3 Select the phone model and protocol for a particular user's phone.
- 5.4 Enter a name for the profile.
- 5.5 Configure user-specific settings, including DN, button customizations, and other parameters.

Figure 11-3 shows a Device Profile Configuration page.

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_325_0.png)

### 11-3 Device Profile Configuration Page

### Step 5b: Subscribe Device Profiles to the EM Service

- 5b.1 From the Device Profile page, choose Subscribe/Unsubscribe Services from the Links pull-down and click Go.
- 5b.2 Choose the EM service added in Step 3 and click Next.
- 5b.3 Enter the display name for the EM service and an ASCII version if needed for phones with low-resolution displays.
- 5b.4 Subscribe, and then click Save.

**Note:** If the Enterprise subscription checkbox was selected in Step 3, Step 5b is not required.

Figure 11-4 illustrates this procedure.

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_326_0.png)

Figure 11-4 Subscribe Device Profile to EM Service

Note: You must subscribe both the Device Profiles and the IP Phones to the EM service. If you do not, the user won't have access to the EM service after she logs in and will not be able to log out.

### Step 6: Associate Users with Device Profiles

- 6.1 Navigate to User Management > End User.
- 6.2 Select the user for whom you want to create profile association, or, if necessary, create a new user (see Chapter 9, “Managing Endpoints and End Users”).
- 6.3 In the user configuration, choose the Device Profile(s) that should be associated with the user. If more than one is assigned, the user must select the one she wants after logging into EM. The Default Profile puts the selected profile at the top of the list.

Figure 11-5 illustrates associating an end user with a Device Profile.

![](img/e4ad7862dc47b4e5de0cde3b45327.png)

Figure 11-5 Associating an End User to Device Profile

### Step 7a: Enable EM for Phones

- 7a.1 Navigate to Device > Phone and select the phone you want to configure for EM.
- 7a.2 In the Extension Mobility section, check the Enable box.
- 7a.3 Choose either specific Device Profile or the currently configured device (recommended) in the Log Profile pull-down.

Note: The Log Profile is the configuration that is applied to the phone when logged into it. Often this profile includes emergency, internal, and sometimes local calling capabilities.

Figure 11-6 shows the phone configuration for EM.

### Step 7b: Subscribe Phones to EM Service

- 7b.1 In the phone configuration, choose Subscribe/Unsubscribe Services from the Related Links pull-down to open the Subscribed Cisco Phone Services window. (This is not necessary if the Enterprise Subscription checkbox is selected in the EM Service Parameters pages.)
- 7b.2 Choose the EM service from the Select Service pull-down.
- 7b.3 Enter the name of the service you want to appear on the IP Phone.

![](img/e4ad7862dc47b4e5de0cde3b45328.0.png)

Figure 11-6 Configuring the Phone for EM

You should be able to go to any phone you have subscribed to the EM service and log in as any user you have configured with a Device Profile for that type.

Figure 11-7 illustrates the EM Service to a phone.

![](img/e4ad7862dc47b4e5de0cde3b45329.0.png)

Figure 11-7 Subscribing the Phone to the EM Service

## Describe Telephony Features in CUCM

CUCM supports a wide range of telephony features. This section reviews some of the widely used features, including several Call Coverage Options, Intercom, and Presence.

### Call Coverage

Call Coverage is a general term that references several features and mechanisms used to ensure calls are answered under any unforeseen circumstances. CUCM supports the following Call Coverage features:

- Call Forward
- Shared Lines
- Call Pickup
- Call Hunting

### Call Forward

There are several Call Forward options configurable in CUCM:

- Call Forward All (CFA): CFA calls all calls to be forwarded to the destination number specified by the user or administrator, either at the phone itself or on the CUCM user or administrative web pages, without ringing the original dialed number. When CFA is enabled, the Call Forward Search Space is used and line/device search spaces are ignored. For this reason, the Call Forward Search Spaces should be configured to avoid call failures in a system that uses Custom Partitions and Search Spaces.

Note: If the Voice Mail checkbox is selected, CUCM ignores the destination in the forward setting and Calling Search Space fields and forwards the call to the Voice Mail Pilot number specified in the configured Voice Mail Profile.

### Shared Lines

If two (or more) IP Phones have the same DN configured on one of their lines, calling the DN causes both phones to ring. The first phone to be picked up takes the call; the second phone cannot pick up the call without invoking the Barge feature (if configured). If the first phone places the call on hold, the second phone can pick up the held call.

### Barge and Privacy

If two phones have a shared line configured and one of the phones is using that line, the second phone can force a three-way conference with the first phone using the Barge feature. The conference is hosted on the first phone's built-in conference bridge. (For IP Phone models not supporting a built-in bridge, an external conference bridge can be configured.) When the second phone barges on the call, all parties hear a beep (by default). If the barge fails (typically a lack of conference resources), the barging phone displays an error message.

A Privacy softkey can be configured that, when enabled, prevents barging into a call in progress. Both the Barge and Privacy capabilities can be enabled and disabled both cluster-wide and at the individual phone configuration pages.

### Call Pickup

A DN can be a member of a Call Pickup Group, which is simply a numbered assignment. Three types of Call Pickup can be configured using these Pickup Group assignments:

- Call Pickup: If multiple DNs have the same group number and one of them is ringing, another phone with a DN in the same pickup group can invoke the Call Pickup softkey and the call is immediately extended to that phone instead.
- Group Call Pickup: If two DNs have different Call Pickup Groups and one of them is ringing, the other phone can invoke the GPicup (Group Call Pickup) softkey, dial the group number of the ringing DN, and the call is immediately extended to that phone instead. A variant of this feature called Directed Call Pickup allows a user to enter a specific DN that is ringing to pick up that specific call, rather than the first call that started ringing in the group.
