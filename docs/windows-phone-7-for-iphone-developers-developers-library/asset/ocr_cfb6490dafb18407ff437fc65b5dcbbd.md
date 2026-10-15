If you choose Pin to Start when prompted, the emulator takes you back to the home screen, and there you will see your tile. If you do not have any other tiles installed, your screen might look something like the one in Figure 11.3.

![](bbox=[0.395, 0.176, 0.678, 0.522])

Now when users unlocks their device, they will see a nice big tile for your application. They can tap this tile to launch the application or launch the application manually by using the right arrow and clicking the application’s title in the list that appears.

The default background that comes with the new application template is a 173x173 24-bit PNG file. When creating your own background images for your applications, you must stick to this convention. Home screen tiles (at least those created by regular non-Microsoft developers) are always the same size and must never exceed 80KB in size.

# Working with Tile Schedules

Many applications will be satisfied using the tile surface as nothing more than a large icon; a place for branding and a super-large hit target for fingers to tap. However, depending on the type of application you’re writing, you might want to do more than that. You might want to make your application tile somewhat dynamic. Note that I say somewhat here, because we’ll talk about how to make your tile much more dynamic in the next chapter when I talk about push notifications.

Tile schedules are at the mercy of the phone itself. You can create an instance of a tile schedule that will cause your application tile to update once, every week, every day, or