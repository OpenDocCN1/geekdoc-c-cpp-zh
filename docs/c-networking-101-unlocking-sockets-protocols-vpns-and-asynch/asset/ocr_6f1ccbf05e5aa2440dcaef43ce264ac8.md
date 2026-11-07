```
```text
use                 local-service
host_name           my-host
service_description SSH
check_command       check_ssh
}

define service{
    use                 local-service
    host_name           my-host
    service_description HTTP
    check_command       check_http
}
```
```

# Add Configuration File to Nagios