# How It Works

The provisioning profile associates one or more development certificates with one or more devices, and an App ID so that you can install your signed iPad application on a real iPad.

# Provisioning a Device

With the provision profile created, you will now install it onto a real device. Once a device is provisioned, your signed iPad application will be able to run on your iPad.

# TRY IT OUT  Provisioning a Device

+   1. Connect your iPad to your Mac.
+   2. Drag and drop the downloaded `MyDevicesProfile.mobileprovision` file onto the Xcode icon on the Dock.
+   3. Launch the Organizer application from within Xcode and select the device currently connected to your Mac. You should see the `MyDevicesProfile` installed on the device.

# How It Works

All devices that you want to test your application on must be provisioned. If a device is not provisioned, you will not be able to install your application on it.

# CREATING THE IPAD APPLICATION

Finally, you can write your iPad application to receive push notifications. The following Try It Out shows how you can programmatically receive notifications received from the APNs server.

# TRY IT OUT  Creating an iPad Application

+   1. In Xcode, create a new View-based Application project and name it `ApplePushNotification`.
+   2. Drag and drop a WAV file (shown as `beep.wav` in this example) onto the Resources folder in Xcode (see Figure 17-21)
+   3. Expand on the Targets item in Xcode and select the `ApplePushNotification` item. Press Command-i. Then, in the info window, click the Properties tab (see Figure 17-22).

![](bbox=[0.6, 0.8, 0.9, 0.93])