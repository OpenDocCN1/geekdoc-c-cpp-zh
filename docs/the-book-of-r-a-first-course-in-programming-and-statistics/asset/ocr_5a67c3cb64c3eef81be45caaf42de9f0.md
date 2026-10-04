This new window will be numbered 3 (it usually sits itself on top of the previously open window, so you may want to move it to one side with your mouse). Importantly, you'll see that this becomes the active device: on a Mac the [*] is now on the Device 3 banner; in Windows, Device 3 will say (ACTIVE), and Device 2 will now say (inactive).

At this point, you can enter the usual command to bring up the desired histogram in Device 3:

```
R> hist(quakes$$stations)
```

If you hadn't used dev.new, the histogram would've just overwritten the plot of the spatial locations in Device 2.

# 23.1.2 Switching Between Devices

To change something in Device 2 without closing Device 3, use dev.set followed by the device number you want to make active. The following code activates Device 2 and replots the locations of the seismic events so that the size of each event is proportional to the number of stations that detected the event. It tidies up the axis labels.

```
R> dev.set(2)
quartz
2
R> plot(quakes$$long,quakes$$lat,0.02+quakes$$stations, xlab="Longitude",ylab="Latitude")
```

Using dev.set always confirms the newly active device by printing to the console; the specific text will vary according to your operating system and type of device.

Switching back to Device 3, as a final tweak, add a vertical line marking the mean number of detecting stations.

```
R> dev.set(3)
quartz
3
R> abline(v=mean(quakes$$stations),lty=2)
```

Figure 23-1 shows the two graphics devices after making these changes.