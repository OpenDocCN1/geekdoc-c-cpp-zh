```
{
    try
    {
        s_ServiceHost = new
ServiceHost(typeof(RoomReservationService),
            new Uri("http://localhost:9000/RoomReservation"));
        s_ServiceHost.Description.Behaviors.Add(
            new ServiceMetadataBehavior
            {
                HttpGetEnabled = true
            });
        myServiceHost.Open();
    }
    catch (AddressAccessDeniedException)
    {
        WriteLine("either start Visual Studio in elevated admin"
+
            "mode or register the listener port with
netsh.exe");
    }
}

internal static void StopService()
{
    if (s_ServiceHost != null &&
        s_ServiceHost.State == CommunicationState.Opened)
    {
        s_ServiceHost.Close();
    }
}

static void Main()
{
    StartService();

    WriteLine("Server is running. Press return to exit");
    ReadLine();

    StopService();
}
}
```

For the WCF configuration, you can copy the application configuration file created with the service library to the host application. You can edit this configuration file with the WCF Service Configuration Editor (see Figure 44.5).