# Create Host and Service Definition Files

First, we need to create configuration files for our host and services. These will be placed in the /usr/local/nagios/etc/objects directory. Let us say we want to monitor a host named my-host.

Create a new configuration file:

```
sudo nano /usr/local/nagios/etc/objects/my-host.cfg
```

In this file, add the following to define your host:

```
define host{

    use              linux-server

    host_name        my-host

    alias            My Host

    address          192.168.1.10

}
```