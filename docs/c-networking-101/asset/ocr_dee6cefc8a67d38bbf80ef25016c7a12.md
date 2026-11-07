```
echoClient.SetAttribute ("PacketSize", UintegerValue (1024));
```

```
ApplicationContainer clientApps = echoClient.Install (nodes.Get (1));
```

```
clientApps.Start (Seconds (2.0));
```

```
clientApps.Stop (Seconds (10.0));
```

# Run the simulation

Finally, we run the simulation:

```
ns3::Simulator::Run ();
```

```
ns3::Simulator::Destroy ();
```

# Build and run

To build and run your simulation, use the ./waf command in the NS-3
directory:

```
./waf --run simple-network
```

And we are done. This is easily doable network simulation with two nodes
communicating over a point-to-point link. The NS-3 framework is
incredibly flexible and powerful, and you can create far more complex