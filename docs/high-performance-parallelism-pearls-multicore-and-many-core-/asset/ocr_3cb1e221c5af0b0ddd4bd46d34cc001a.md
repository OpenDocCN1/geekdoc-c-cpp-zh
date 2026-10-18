```
LoadPlugin network
LoadPlugin mic

<Plugin network>
Server "cluster-collectd" "25826"
ReportStats false
</Plugin>
<Plugin mic>
    ShowCPU true
    ShowCPUCores false
    ShowMemory true
    ShowTemperatures true
    ShowPower true
</Plugin>
```

# FIGURE 25.12

collectd.conf snippet showing network data send and a plugin for the coprocessor.

```
<LoadPlugin python>
Globals true
</LoadPlugin>
LoadPlugin Network
<Plugin network>
Listen "cluster-collectd" "25826"
ReportStats false
</Plugin>

<Plugin python>
ModulePath "/usr/lib/python2.6/site-packages/nwperf"
Import nwcollectd
    <Module nwcollectd>
        NameServer "tcp://nwperf-ns:6967"
        ClusterName "cascade"
        IP "192.168.1.1"
    </Module>
</Plugin>
```

# FIGURE 25.13

collectd.conf snippet showing network data send.

python plugin will register with the nwperf nameservice defined in the config file. In Figure 25.13, we show that a cluster name and an IP address for external connection need to be specified. We will use the cluster name “cascade” throughout this example.

3. Configure long-term storage. In order for NWPerf to gather and collect the data in long-term storage, in this example, we use a ceph object store pool. This assumes you have ceph running and can create a new pool according to the instructions on the NWPerf Website. Once nwperf is installed on the server that will be processing data, we run a few configuration commands to modify some of the defaults in the /etc/nwperf.conf file (see Figure 25.14).

The default assumes the hostname “nwperf-ns” is setup in /etc/hosts or DNS, so that all services can talk to the NWPerf nameservice. Once you have started the nwperf services and have