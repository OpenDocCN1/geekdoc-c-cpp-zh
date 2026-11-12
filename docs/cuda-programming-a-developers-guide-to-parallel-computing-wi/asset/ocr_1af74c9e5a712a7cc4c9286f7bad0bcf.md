![](bbox=[0.136, 0.118, 0.886, 0.268])

# FIGURE 4.10 Parallel Nsight connected remotely.

The next step is to run Visual Studio on the host PC and select a new analysis activity. You will see a section near the top of the window that looks like Figure 4.9. Notice the “Connection Name” says localhost, which just means your local machine. Open Windows Explorer and browse the local network to see the name of the Windows PC you would like to use to remotely debug. Replace localhost with the name shown in Windows Explorer. Then press the “Connect” button. You should see two confirmations that the connection has been made as shown in Figure 4.10.

First, the “Connect” button will change to a “Disconnect.” Second, the “Connection Status” box should turn green and show all the possible GPUs on the target machine (Figure 4.11). In this case we’re connecting to a test PC that has five GTX470 GPU cards set up on it.

![](bbox=[0.375, 0.53, 0.64, 0.785])

# FIGURE 4.11 Parallel Nsight connection status.

Clicking on the “Launch” button on the “Application Control” panel next to the “Connection Status” panel will remotely launch the application on the target machine. However, prior to this all the necessary files need to be copied to the remote machine. This takes a few seconds or so, but is all automatic. Overall, it’s a remarkably simple way of analyzing/debugging a remote application.