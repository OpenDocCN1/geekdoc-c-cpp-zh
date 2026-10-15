
## Launching the Phone Application

As mentioned at the beginning of this section, Windows Phone 7 will not allow any application you write to have direct access to the phone features. This is to keep the cellular network (and the people using it) from being abused. A compromise is to allow your applications to suggest to the phone a phone call that it would like to make. This then brings up a dialog that a user must confirm in order to place the call, as shown in Figure 10.5.

```
PhoneCallTask phoneCall = new PhoneCallTask();
phoneCall.DisplayName = "Jenny";
phoneCall.PhoneNumber = "8675309";
phoneCall.Show();
```

![](img/04a00d46bb1059867d95707babd62ee7_144_0.png)

Figure 10.5 Placing a call with the PhoneCallTask.

## Sending a Text Message

The same reasoning behind limiting direct access to phone functionality prevents us from being able to directly send text messages. If you want your users to be able to send an SMS from your application, you can utilize the SmsComposeTask as shown in the following code (see Figure 10.6). The iPhone allows applications to send text messages through the use of an MFMessageComposeViewController that works in a nearly identical fashion.

```
SmsComposeTask newSms = new SmsComposeTask();
newSms.To = "Jenny Jenny";
newSms.Body = "Who can I turn to?";
newSms.Show();
```

![](img/04a00d46bb1059867d95707babd62ee7_145_0.png)

Figure 10.6 Sending a text message with the SmsComposeTask.

## Composing an Email Message

If the Windows Phone 7 device has at least one configured mail account, emails can be created programmatically. Again, because you are accessing system-level services, the user must provide final confirmation before sending the email.

To create a new email message from your application, use the EmailComposeTask as shown next.

```
EmailComposeTask newEmail = new EmailComposeTask();
newEmail.To = "Jenny Jenny";
newEmail.Subject = "I got it";
newEmail.Body =
@"For a good time, for a good time call....";
newEmail.Show();
```

## Using Choosers

For the same reason that devices cannot allow developers to directly manipulate data and system-level services, developers are often prevented from querying or reading detailed, low-level information. This is for the protection of the consumer as much as it is for the protection of the device manufacturer and cellular carrier. To be able to guarantee consumers, carriers, and device manufacturers that rules and legal obligations with regard to

data security and isolation have been met, Windows Phone 7 (and iOS) cannot allow developers to crack open the system databases and browse freely.

The compromise is the use of choosers. Whenever an application wants to allow the user to locate information of a certain kind on the system, the chooser provides a standard user interface that is designed to require the confirmation of the end user before the information is made available to the application. This section will take you on a quick tour through some of the choosers available in Windows Phone 7.

## Using the Phone Number Chooser Task

The phone number chooser task, as its name implies, allows your users to select a phone number from among the phone’s stored contacts. This might be used in conjunction with the launcher that will allow a user to initiate a phone call. Your application might occasionally need to prompt the user to select a phone number from one of the contacts stored on the phone and this chooser task provides that functionality.

To do this, make use of the PhoneNumberChooserTask as shown next:

```
PhoneNumberChooserTask phoneChooser = new PhoneNumberChooserTask();
phoneChooser.Completed += (s, e) =>
{
    if (e.TaskResult == TaskResult.OK)
    {
        MessageBox.Show("You picked " + e.PhoneNumber);
    }
    else
        MessageBox.Show("You didn’t pick anyone");
};
phoneChooser.Show();
```

## Using the Email Address Chooser Task

To prompt the user to select an email address (which is returned to your application in the form of a string) from an existing contact, you use the EmailAddressChooserTask as shown next:

```
EmailAddressChooserTask emailChooser = new EmailAddressChooserTask();
emailChooser.Completed += (s, e) =>
{
    if (e.TaskResult == TaskResult.OK)
    {
        MessageBox.Show("You picked email: " + e.Email);
    }
    else
```

```
MessageBox.Show("You didn't pick anyone.");
};
emailChooser.Show();
```

## Choosing or Capturing Photos on the Device

To prompt the user to select a picture from the phone’s photo library, you can use the PhotoChooserTask. This task comes with an option called ShowCamera, which gives the user the option to take a picture when prompted by your application for a photo. For example, an expense report application might prompt the user for a photo, and the user can either pull up a previously taken picture of a receipt or take a new photo. Regardless of the original source of the image, the picture the user selects is made available to the application in the ChosenPhoto property of the event arguments.

```
PhotoChooserTask photoChooser = new PhotoChooserTask();
photoChooser.ShowCamera = true;
photoChooser.Completed += (s, e) =>
{
    if (e.TaskResult == TaskResult.OK)
    {
        BitmapImage bmp = new BitmapImage();
        bmp.SetSource(e.ChosenPhoto);
        targetImage.Source = bmp;
    }
};
photoChooser.Show();
```

The previous code converts the ChosenPhoto property (which is a stream) into a BitmapImage, which can then be set as the source of an Image control (declared in XAML as <Image/>). Figure 10.7 shows a sample screen the user might see when being prompted to choose a picture from the camera’s media library. At the bottom of this image you can see an icon of a camera. Tapping this will bring up a capture screen for the phone’s embedded camera.

![](img/04a00d46bb1059867d95707babd62ee7_148_0.png)

## Using Hardware Services and Sensors

So far, you’ve seen how to use “soft” services such as choosers and launchers. These facilities allow your application to interact with system-level data and services in a safe way that never allows your application to do, see, or modify anything without the explicit consent of the user.

This next section takes you through using some actual hardware services, such as the accelerometer, the phone vibration controller, using an FM radio tuner, and of course, using the GPS.

### Controlling Vibration

Windows Phone 7 devices have the capability to vibrate. Most modern cell phones have the option of vibrating instead of playing an audible ringtone to make the devices less obtrusive in public places. This has become a blessing in recent years as the people who have cell phones vastly outnumber those who do not.

A nice feature in the Windows Phone 7 SDK is the capability for your application to start and stop vibration on the phone. This gives you the capability to vibrate the phone when something important happens, like a message arriving or a player scoring a point in a game.

To utilize this functionality, you need to make sure your project has a reference to the Microsoft.Devices assembly. If it doesn’t already have this reference, right-click the References node in the project explorer, click Add Reference, and choose the Microsoft.Devices library. Then add the following line of code to the top of whatever page you want to vibrate:

```
using Microsoft.Devices;
```

Now add the following code to start vibration (and continue vibrating for a set amount of time):

```
VibrateController.Default.Start(TimeSpan.FromSeconds(1));
```

If you want to force vibration to stop at any time, call the Stop method, as shown here:

```
VibrateController.Default.Stop();
```

## Accessing a Radio Tuner

In this age of Internet radio, satellite radio, and hundreds of other ways to stream music to your mobile device over cellular data networks or Wi-Fi, you might be thinking, “FM radio? What’s that?”

Whether you agree with the decision or not, Windows Phone 7 devices have the capability to support an FM radio tuner, and the Windows Phone 7 SDK has the capability to control this tuner.

The following bit of code will turn the radio on, tune it to 96.5, and report the radio signal strength in RSSI units. If you have tried out no other code sample in this chapter, I highly recommend you try this one out in the simulator. If you’re expecting the simulator to report that the FM radio is disabled on this device, that’s all the more reason for you to run this sample on your own. Seriously, go type this in and run it. The book will still be here when you get back.

Remember that your project will need a reference to the Microsoft.Devices assembly for the following code to work:

```
try
{
    FMRadio radio = Microsoft.Devices.Radio.FMRadio.Instance;
    radio.Frequency = 96.5;
    radio.PowerMode = RadioPowerMode.On;
    Debug.WriteLine("Radio signal strength : {0}", radio.SignalStrength);
}
catch (RadioDisabledException rde)
{
    MessageBox.Show("the radio is not available on this device.");
}
```
