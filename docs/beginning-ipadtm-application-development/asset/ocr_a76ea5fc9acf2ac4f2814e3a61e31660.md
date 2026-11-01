# 17

# Apple Push Notification Services

# WHAT YOU WILL LEARN IN THIS CHAPTER:

+   - Understand how to use the Apple Push Notification service
+   - How to generate a certificate request
+   - How to generate a development certificate
+   - How to create an App ID
+   - How to configure App ID for push notification
+   - How to create a provisioning profile
+   - How to provision a device
+   - How to deploy an iPad application onto a device
+   - How to use a push notification provider application

One of the key limitations of the iPad is its constraint on running applications in the background, which means that applications requiring a constant state of connectivity (such as social networking applications) will not be able to receive timely updates when the user switches to another application.

To overcome this limitation, Apple released the Apple Push Notification service (APNs). APNs allows your device to be constantly connected to Apple's push notification server. When you want to send a push notification to an application installed on the users' devices, you (the provider) can contact the APNs so that it can deliver a push message to the particular application installed on the intended device.