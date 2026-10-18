
benchmark while micro-tuning for a Green500 submission; to do this, Intel employed a specific process (not discussed at length here) that used power meters for node measurement and calibration, the `micsmc` utility for coprocessor power measurement, and IPMI for automated node measurement.

## WATERFALL CHARTS GENERATED WITH CVIEW FROM NWPerf DATA

NWPerf collects performance utilization data (processor and I/O subsystems) as well as power consumption data, and stores it in a centralized database. Two user interactive systems are available to display the data:

- 1. `NWPerf` provides a user web service for displaying their jobs, allowing display and comparison with 2D graph views. This provides cluster users a personalized view of where and how their jobs are running. NWPerf is built and designed to work on Linux.
- 2. The other tool is `CView`; it provides the 3D waterfall charts shown in this chapter. Waterfall charts allow for a more extensive representation of in-progress work across multiple dimensions (e.g., time, power consumption, resource consumption, and systems to name a few). CView is developed primarily on Ubuntu Linux systems, but Redhat, Microsoft Windows, and OS X build environments work as well.

The waterfall charts generated shown in this chapter are created using the `CView` tool.

Overall, at a high level, the following ingredients are used for data collection, integration and viewing; these are described in greater detail below:

- 1. A data collection mechanism (`collectd` or `ganglia`) is installed on all compute nodes.
- 2. A cluster-`collectd` node receives the data from compute nodes and funnels it into a NWPerf “service.”
- 3. An `NWPerf` instance subscribes to this data service and stores the data in a ceph object store (storage).
- 4. The `gen_cview` tool runs every minute to collect 2 hours of ceph data; creating data-sets for `CView`.
- 5. `CView` is run on endpoint (client) systems.

The aforementioned functions 2-4 could technically all reside on the same server in a small cluster environment. For larger clusters, we recommend separating where cluster-collectd, NWPerf, and gen_cview are run.

## INSTALLING AND CONFIGURING NWPerf AND CView

In order to deploy a full `NWPerf` to `CView` visualization system, you need to start by deploying a data collection tool in the cluster itself. For this example, we will use the `collectd` tool, though similar steps can be taken when using ganglia for data collection.

- 1. Install `collectd` on all cluster compute nodes. Direct all nodes to channel data to a centralized `collectd` node, setting the hostname as appropriate, and configuring the Intel MIC plugin to collect additional data for the coprocessors; changes to `collectd.conf` are shown in Figure 25.12.
- 2. Install `collectd` and `NWPerf` on the central “cluster-collectd” node. The configuration allows for data to be accepted from the network, and then published as an nwperf service. The `nwcollected`

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

### FIGURE 25.12

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

### FIGURE 25.13

collectd.conf snippet showing network data send.

python plugin will register with the nwperf nameservice defined in the config file. In Figure 25.13, we show that a cluster name and an IP address for external connection need to be specified. We will use the cluster name “cascade” throughout this example.

3. Configure long-term storage. In order for NWPerf to gather and collect the data in long-term storage, in this example, we use a ceph object store pool. This assumes you have ceph running and can create a new pool according to the instructions on the NWPerf Website. Once nwperf is installed on the server that will be processing data, we run a few configuration commands to modify some of the defaults in the /etc/nwperf.conf file (see Figure 25.14).

The default assumes the hostname “nwperf-ns” is setup in /etc/hosts or DNS, so that all services can talk to the NWPerf nameservice. Once you have started the nwperf services and have

```
#Specify a cluster name
nwperfconfig -a cluster -v <cluster name>
#Setup a periodic data set dump.
nwperfconfig -a gen_cview.command -v "gen_cview -c %(cluster) -o /dev/shm/%(cluster) -r 60 "
#Specify which nwperf workers to start
nwperfconfig -a services -v gen_cview,nwperf=ceph+store,nwperf=ns
#start Services
restart nwperf
```

### FIGURE 25.14

nwperf configuration commands to setup services based on the installed defaults.

collectd running a nameservice query is possible: as an example “nwperf-nsq.py tcp://nwperf ns:6967 listServices,” should return “cascade.allpoints.” The ceph processing program subscribes to this service to store data in the ceph pool.

- 4. **Install CView.** Download the CView source, compile and install it according to the README instructions, using cmake.
- 5. **Create a CView configuration file.**

First, create a basic CView file by running the cviewall tool:

```
cviewall -url http://lotsofcores.com/power/cview1/ -metrics ‘(mic-0/cpu-user,mic-1/cpu-user)’
```

This is one sample data set we provided. Please visit http://lotsofcores.com/power for more tips, and information on several different collections of data and how to view them using cviewall. You are encouraged to take cviewall for a spin!

To interact with CView, use the keys w, a, s, d, arrow keys, pgup, pgdown, and mouse buttons to move the graphics around and view them. If you have the AntTweakBar library installed, you can press “t” to get access to various control windows. Once you have a configuration that meets your needs, you can press “z” for a screenshot, or “~” to dump the configuration to a file. This config text file, defaults to the name “cviewall.cview,” uses the Apple plist format, and can be modified to suit your specific needs. Once you have a configuration file, you can run “cview -c <configfile>” to start up CView using the saved configuration. Many modifications can be done to this file to split the window into multiple areas, or to do data calculations. A sample config file showing multiple clusters, with calculations, is available on the http://lotsofcores.com site as part of the downloads for this chapter.

The gen_cview tool is run regularly to dump the most recent 2 h CView to /dev/shm/<cluster name>, using the data in ceph as configured and described above. This same tool can be used to generate data sets using historical data using the selection and summation options on the command line.

The data in /dev/shm/<cluster name> data can be provided to a Web server, or directly accessed by the CView program. A wsgi python module for the Web server can also pull this data as needed and is included in the NWPerf codebase. Once a Web server is configured to serve these files, we can then access this data with CView from any client (Figure 25.15).

In a production environment, you can set up and configure kiosks to support the interactive consumption of this pre-configured data for administrators and users. These kiosks can display a waterfall graph of time series performance metrics. They can also support the inclusion of text, images, bar

![](img/16cb41208935c5f22dd1044f03f2e31b_553_0.png)

### FIGURE 25.15

Cluster usage data visualization on multiple screens.

graphs, InfiniBand cable maps, etc. Data for the waterfall chart can be input from a defined CView data set, or from streaming command line data. CView supports continuous reloads so that waterfall graphs can offer up-to-the-minute data for real-time analysis. The 3D views represented through waterfall charts in CView can be manipulated and navigated using mouse and keyboard commands, as previously described.

Multiple waterfall charts can be displayed on a single screen using a grid-like layout system, for example, one can put different data on each screen of a multiple-monitor system to correlate various aspects of a cluster’s resource consumption as seen in Figure 25.15.

## INTERPRETING THE WATERFALL CHARTS

Each waterfall plot can display multiple dimensions of data. A typical use case is to plot data for each node in a cluster, over a period of time, with the third dimension representing resource consumption such as power or memory use. The consumption can be represented like a heat map, so the eye can easily decipher where problem spots exist. Thus, as seen in Figure 25.16, the X axis in a waterfall plot may be cluster nodes; the Y axis is time; and the Z axis is power consumption (in watts). Color-coding the resource consumption (in this case, power) where the color blue represents a “cooler” temperature, and yellow to red represents continuously “hotter” temperatures allows fast interpretation of cluster node power consumption. In gray scale, the waterfall charts represent the highest resource consumption in lighter shades (toward white) plus greater height across the Y axis. The color versions of these waterfall charts are available on http://lotsofcores.com as part of download of figures from this book. Correlating power data with separate graphs showing jobs run by different users, and with charts representing CPU and I/O consumption, we can determine which jobs make inefficient resource use and/or which jobs may have changed in behavior over time. A change in behavior might be an indication of modifications resulting in worse power consumption and performance compared to historical measurements.
