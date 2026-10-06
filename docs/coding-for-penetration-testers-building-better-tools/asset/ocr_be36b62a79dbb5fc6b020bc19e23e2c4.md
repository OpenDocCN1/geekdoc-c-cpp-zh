```
for ($counter=$start; $counter -le $stop; $counter++)
{
    write-output "testing port $counter on $device"
    $porttest = new-object Net.Sockets.TcpClient
    try{
        $connect = $porttest.connect($device,$counter)
        write-output "$counter is open"
    }catch{
        write-output "$counter is closed"
    }
}else{#this branch checks a single port
    write-output "testing port on $device"
    $porttest = new-object Net.Sockets.TcpClient
    try{
        $connect = $porttest.connect($device,$port)
        write-output "$port is open"
    }catch{
        write-output "$port is closed"
    }
}

#run our functions
pingdevice
checkpoints
```

Looking at the code listing, we can see a variety of structures discussed in this section, plus a few new things thrown in for variety. The first new thing we see, since our script is getting a bit more sizable, is a comment. We can use the # character to indicate we do not want the interpreter to do anything with that line or portion of the line. We can put comment marks at the beginning of the line, or anywhere in the middle, and everything after it will be ignored.

The next line of the script takes any arguments passed to the script and puts them into the variables we'll use later. The $device variable we can always expect to be an IP address or domain name, but the other three may vary or not be used at all, as we'll see in one of our functions.

The pingdevice function will check to make sure the IP or domain named in our $device variable is actually up on the network. The function contains a simple statement and uses the test-connection cmdlet in order to ping the device. We also use the -