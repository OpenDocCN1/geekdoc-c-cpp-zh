![](bbox=[0.14, 0.1, 0.72, 0.32])

# Figure 6.4

Next, click the drop-down menu in the upper-left corner of Xcode, make sure it is set to “Debug,” and then select the simulator you want to run. It’s best to select the most current simulator (iPhone 4.0), because that is the device that most people will have. It is also a good idea to ensure that the simulator runs on all platforms. For example, if you select iPad as your simulator, it will run the app as an iPhone app, not an iPad app, and so the app will appear significantly smaller than it would normally (figure 6.5). You are now ready to build the app. Click the “Build and Run” button.

![](bbox=[0.5, 0.36, 0.77, 0.61])

# Figure 6.5

![](bbox=[0.09, 0.61, 0.21, 0.66])

After about ten seconds the simulator will launch, and your app will appear. If it does not launch and you see red or yellow flags in the lower-right side of the screen, click on the flags to examine the message. You will notice two things the first time the app loads. First, the icon is for PhoneGap; second, the loading image reads “PhoneGap.” Let’s see how to get rid of those two graphics and replace them with library images. Close the Xcode program and simulator. Now, let’s make an iPhone app icon. It’s simple. Create an image with a dimension of 57 × 57; use the file name “icon.png” to save the image. Move the file you created into the PhoneGap and iPhone directory. The file will replace the already-created “icon.png” and replace it with your new one. Next, let’s change the start-up image. Repeat the steps to create an icon, except this time name your image “Default.png” and make sure it has the following dimensions: 320 × 480. Move this image into the PhoneGap and iPhone directory.