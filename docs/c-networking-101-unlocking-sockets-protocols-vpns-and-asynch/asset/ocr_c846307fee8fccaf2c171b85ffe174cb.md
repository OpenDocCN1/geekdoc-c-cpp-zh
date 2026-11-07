```
AUTH_LOG=/var/log/auth.log

# Count the number of successful SSH log-ins in the last day

SUCCESS_COUNT=$(grep -i "Accepted password" $AUTH_LOG | grep "$(date '+%b %e')" | wc -l)

# Count the number of failed SSH log-ins in the last day

FAIL_COUNT=$(grep -i "Failed password" $AUTH_LOG | grep "$(date '+%b %e')" | wc -l)

echo "SSH Log-ins: $SUCCESS_COUNT successful, $FAIL_COUNT failed"
```

# Set up the Script as a Nagios Plugin

To use this script as a Nagios plugin, you first need to move it to the directory where Nagios keeps its plugins, usually /usr/lib/nagios/plugins. You should also make sure the script is executable by running:

```
chmod +x script_name.sh.
```