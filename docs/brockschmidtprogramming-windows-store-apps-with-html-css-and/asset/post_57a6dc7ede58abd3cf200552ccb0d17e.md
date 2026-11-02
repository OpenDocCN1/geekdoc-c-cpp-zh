
## Connectivity Events

It is very common for a running app to want to know when connectivity changes. This way it can take appropriate steps to disable or enable certain functionality, alert the user, synchronize data after being offline, and so on. For this, apps need only watch the `onnetworkstatuschanged` event of the `NetworkInformation` object, which is fired whenever there's a significant change within the hierarchy of objects we've just seen (and be mindful that this event comes from a WinRT object, so remove your listeners properly). For example, the event will be fired if the connectivity level of a profile changes or the network is disconnected. It fires when new networks are found, in which case you might want to switch from one to another (for instance, from a metered network to a nonmetered one). It will also be fired if the Internet profile itself changes, as when a device roams between different networks, or when a metered data plan is approaching or has exceeded its limit, at which point the user will start worrying about every megabyte of traffic.

In short, you'll generally want to listen for this event to refresh any internal state of your app that's dependent on network characteristics and set whatever flags you use to configure the app's networking behavior. This is especially important for transitioning between online and offline and between unlimited and metered networks; Windows, for its part, also watches this event to adjust its own behavior, as with the Background Transfer APIs.

**Note** Windows Store apps written in JavaScript can also use the basic `window.navigator.online` and `window.navigator.onoffline` events to track connectivity. The `window.navigator.online` property is also true or false accordingly. These events, however, will not alert you to changes in connection profiles, cost, or other aspects that aren't related to the basic availability of an Internet connection. For this reason it's generally better to use the WinRT APIs.

You can play with `networkstatuschanged` in scenario 5 of the Network information sample. As you connect and disconnect networks or make other changes, the sample will update its details output for the current Internet profile if one is available (code condensed from `js\network-status-change.js`):

```javascript
var networkInfo = Windows.Networking.Connectivity.NetworkInformation;
// Remember to removeEventListener for this event from WinRT as needed.
networkInfo.addEventListener("networkstatuschanged", onNetworkStatusChange);

function onNetworkStatusChange(sender) {
    internetProfileInfo = "Network Status Changed: \n\r";
    var internetProfile = networkInfo.getInternetConnectionProfile();

    if (internetProfile === null) {
        // Error message
    } else {
        internetProfileInfo += getConnectionProfileInfo(internetProfile) + "\n\r";
        // display info
    }

    internetProfileInfo = "";
}
```

Of course, listening for this event is useful only if the app is actually running. But what if it isn't? In that case an app needs to register a background task for what's known as the `networkStateChange` trigger, typically applying the `internetAvailable` or `internetNotAvailable` conditions as needed. We'll talk more about background tasks in Chapter 16; for now, refer to the Network status background sample for a demonstration. The sample simply retrieves the Internet connection name and network adapter id in response to this trigger; a real app would clearly take more meaningful action, such as activating background transfers for data synchronization when connectivity is restored. The basic structure is there in the sample nonetheless.

It's also very important to remember that network status might have changed while the app was suspended. Apps that watch the `networkstatuschanged` event should also refresh their connectivity-related state within their resuming handler.

As a final note, check out the Troubleshooting and debugging network connections topic, which has a little more guidance on responding to network changes as well as network errors.

## Cost Awareness

If you ever crossed between roaming territories with a smartphone that's set to automatically download email, you probably learned the hard way to disable syncing in such circumstances. I once drove from Washington State into Canada without realizing that I would suddenly be paying $15/megabyte for the privilege of downloading large email attachments. Of course, since I'm a law-abiding citizen I did not look at my phone while driving (wink-wink!) to notice the roaming network. Well, a few weeks later and $100 poorer I knew what "bill shock" was all about!

The point here is that if users conclude that your app is responsible for similar behavior, regardless of whether it's actually true, the kinds of ratings and reviews you'll receive in the Windows Store won't be good! If your app might transfer any significant data, it's vital to pay attention to changes in the cost of the connection profiles you're using, typically the Internet profile. Always check these details on startup, within your `networkstatuschanged` event handler, and within your resuming handler.

**Tip** A powerful way to deal with cost awareness is through what's called a filter on which the `Windows.Web.Http.HttpClient` API is built. This allows you to keep the app logic much cleaner by handling all cost decisions on the lower level of the filter. To see this in action, refer to scenario 11 of the HttpClient sample.

You, and all of your customers, I might add, can track your app's network usage in the App History tab of Task Manager, as shown below. Make sure you've expanded the view by tapping More Details on the bottom left if you don't see this view. You can see that it shows Network and Metered Network usage along with the traffic due to tile updates.

hand, when the type is `variable` and the user is paying for every byte, especially when `roaming` is `true`, you'll want to inform the user of that status and provide settings through which the user can limit the app's network activity, not halt that activity entirely. After all, the user might decide that certain kinds of data are worth having. For example, they should be able to set the quality of a streaming movie, indicate whether to download email messages or just headers, indicate whether to download images, specify whether caching of online data should occur, turn off background streaming audio, and so on.

Such settings, by the way, might include tile, badge, and other notification activities that you might have established, as those can generate network traffic. If you're also using background transfers, you can set the cost policies for downloads and uploads as well.

An app can, of course, ask the user's permission for any given network operation. It's up to you and your designers to decide when to ask and how often. Windows Store policy, for its part (section 4.5), requires that you ask the user for any transfer exceeding one megabyte when `roaming` and `overDataLimit` are both `true`, and when performing any transfer over `maxTransferSizeInMegabytes`. I like to think of that policy as a minimum requirement, and your customers will clearly appreciate more consideration, especially if your app is making a number of smaller transfers that might add up to multiple megabytes. At the same time, you don't want to be annoying with consent prompts, so be sure to give the user a way to temporarily disable warnings or ask at reasonable intervals. In short, put yourself in your customer's shoes and design an experience that empowers their ability to control the app's behavior.

On a `fixed` type network, where data is unrestricted up to `dataPlanLimitInMegabytes`, we find cases where a number of the other properties become interesting. For example, if `overDataLimit` is already `true`, you can ask the user to confirm additional network traffic or just defer certain operations until the `nextBillingCycle`. Or, if `approachingDataLimit` is `true` (or even when it's not), you can determine whether a given operation might exceed that limit. This is where the connection profile's `getNetworkUsageAsync` method comes in handy to obtain a `NetworkUsage` object for a given period (see How to retrieve connection usage data for a specific time period). Call `getNetworkUsageAsync` with the time period between `DataPlanUsage.lastSyncTime` and `DateTime.now()`. Then add that value to `DataPlanUsage.megabytesUsed` and subtract the result from `DataPlanUsage.dataPlanLimitInMegabytes`. This tells you how much more data you can transfer before incurring extra costs, thereby providing the basis for asking the user, "Downloading this file will exceed your data plan limit and dock your wallet. Is that OK or would you rather save your money for something else?"

For simplicity's sake, you can think of cost awareness in terms of three behaviors: `normal`, `conservative`, and `opt-in`, which are described on Managing connections on metered networks, and more broadly, on Developing connected apps. Both topics provide additional guidance on making the kinds of decisions described here already. In the end, saving the user from bill shock and designing a great user experience around network costs is definitely an essential investment.
