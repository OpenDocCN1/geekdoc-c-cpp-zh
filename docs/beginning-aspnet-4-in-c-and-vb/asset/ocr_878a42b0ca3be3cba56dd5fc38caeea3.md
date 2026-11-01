When you run the application with at least one peer available for discovery the display will be similar to Figure 45-8

The code is structured in the same way as the previous example, so if you've read through that code you should be familiar with this code. This time there is not much work to do in the Window_Loaded() event handler except sign in, because there is no WCF service to initialize or peer name registration to achieve:

```
private void Window_Loaded(object sender, RoutedEventArgs e)
{
    // Sign in to PNM
    PeerCollaboration.SignIn(PeerScope.NearMe);
}
```

To make things look a little nicer, though, ContactManager.LocalContact.Nickname is used to format the window title:

```
// Get local peer name to display
this.Title = string.Format("PNMSample - {0}",
    ContactManager.LocalContact.Nickname);
```

In Window_Closing() the local peer is automatically signed out of PNM:

```
private void Window_Closing(object sender,
    System.ComponentModel.CancelEventArgs e)
{
    // Sign out of PNM
    PeerCollaboration.SignOut(PeerScope.NearMe);
}
```

Most of the work is done in the RefreshButton_Click() event handler. This uses the PeerCollaboration.GetPeersNearMe() method to obtain a list of peers and add those peers to the display using the PeerEntry class defined in the project, or display a failure message if none are found:

```
private void RefreshButton_Click(object sender, RoutedEventArgs e)
{
    // Get local peers
    PeerNearMeCollection peersNearMe = PeerCollaboration.GetPeersNearMe();

    // Prepare for new peers
    PeerList.Items.Clear();

    // Examine peers
    foreach (PeerNearMe peerNearMe in peersNearMe)
    {
        PeerList.Items.Add(
            new PeerEntry
            {
                PeerNearMe = peerNearMe,
                PresenceStatus = peerNearMe.GetPresenceInfo(
                peerNearMe.PeerEndPoints[0].PresenceStatus,
                DisplayString = peerNearMe.Nickname
            });
    }

    // Add failure message if necessary
    if (PeerList.Items.Count == 0)
    {
        PeerList.Items.Add(
            new PeerEntry
            {
```

![](bbox=[0.65, 0.17, 0.88, 0.32])

FIGURE 45-8