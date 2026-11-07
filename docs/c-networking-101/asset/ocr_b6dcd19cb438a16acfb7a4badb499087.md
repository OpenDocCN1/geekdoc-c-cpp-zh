In the above sample program, remote_host should be replaced with the name of the host as defined in Nagios.

# Verify and Reload Configuration

You should always verify your configuration files before reloading Nagios. This can be done using the nagios -v command, like this:

```
/usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg
```

If the verification process completes without errors, reload Nagios to apply the changes:

```
service nagios reload
```

Now Nagios will start monitoring the CPU load on the remote host, and it will send alerts according to the thresholds you defined. You can view the status of the service and any performance data collected in the Nagios web interface.