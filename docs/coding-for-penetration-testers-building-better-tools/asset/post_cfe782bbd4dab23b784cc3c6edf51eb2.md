
more esthetically pleasing and to monitor their progress, we might want to wrap Netcat in a bit of a script in order to add a few extra features.

For the sake of simplicity and clarity, we'll be splitting the send and receive code into two different scripts. First, let's have a look at the receive code, which we would execute as ./receive (this, of course, we won't do anything until we send something to it with the other piece of script:

```bash
#!/bin/bash
port='80'
port2='443'
filename=default.txt
filename2=$(nc -w 30 -l -p $port2)
filename=$filename2
echo "Incoming filename $filename"
nc -w 30 -l -p $port > $filename
echo "Finished"
```

This is a relatively simple block of code, but we're doing a bit of extra work to make our file transfer somewhat cleaner. In the example we looked at where we did the file transfer on the command line, we had to manually specify the filename on the receiving end to end up in the right place, which is somewhat less elegant. Here, we'll be using two different Netcat transactions in order to avoid having to do this.

The top few lines of our bash script contain the shebang and the setup for our variables. We'll be working with two different ports, 80 to send the actual file over 443 to send the filename. Using the common web ports is somewhat arbitrary, but may keep us from tripping over network or security devices that are blocking other, less common, ports. We also have two variables set up to contain the filename, one of which we will be overwriting.

In our first Netcat transaction, we'll be listening on the port specified in the variable port2, 443 by default. We will take the traffic transmitted to our Netcat listener, hopefully our incoming filename, and place it into filename2. We will then take the value in $filename2 and write it to filename. We would take the input directly from our Netcat listener and put it into filename, but this doesn't leave much room for issues. Using two different filename variables this way gives us a margin for error, and gives us a better chance of ending up with something reasonable (likely default.txt) if we have a problem. Now that we have a filename, we can echo it out and look for the incoming file.

Here we start our Netcat listener, this time on the port specified in our port variable (80). We have the incoming file, naming it for the value in the filename variable which was passed to us earlier. We then echo a statement indicating we are done and exit the script.

Now let's look at the send script, which we would execute as ./send testfile.

```bash
#!/bin/bash
filename=$1
host=$2
port='80'
port2='443'
echo Sending file $filename to $host
echo $filename | nc -w 2 $host $port2
nc -w 2 $host $port2 < $filename
echo "Finished"
```

This script has a similar initial setup as the receive script. First we have the shebang and out block of variables. We take in the name of the file we will be sending and the name of the host we will be sending it to as command line arguments, $1 and $2, respectively. We also set our ports in the port and port2 variables, matching the two port values we set in the receive script. Additionally, we echo out a message to the console to tell the user what file we will be sending and where we will be sending it.

Next, we run our two Netcat transactions. First we send the filename by echoing the contents of the filename variable and piping to Netcat. Netcat will send this to the host and port specified in our host and port2 variables, communicating the name of the file we intend to send so that the receive script can name it properly on the other end. Also note that here, and in the receive script as well, we have dispensed with the -v option for Netcat. Although it is nice to have Netcat be a bit chatty on the command line when we are using it, this is not as helpful in the middle of our script.

We then send the actual file itself over the port specified in port and to the same host as our previous connection. Lastly, we echo out a message to tell the user we have finished. The overall exchange should look something like Fig.7.2.

![](img/42f332b2adf7dab7e681e5d6cdd2074c_281_0.png)

# FIGURE 7.2 Netcat file transfer Send and Receive output.

There are several things we can do to improve our set of scripts here:

- Use one of the Netcat derivatives, such as CryptCat, that supports encryption in order to secure our transmissions.
- Combine the send and receive scripts into one script, and differentiate between sending and receiving functionality through the use of arguments.
- Include the option to use compression tools such as tar and/or gzip so that we don't need to send as much data over the network.
- Consider rewriting the script in a more flexible language such as Perl or Ruby so that we can do more with the information that Netcat is sending or receiving.
- Take in the listening and/or sending ports as an argument so that we are more flexible.
- Add error handling. In the present state of our scripts, it doesn't take much to get us off the rails, and we won't handle issues gracefully.
- Add progress monitoring. We can use a tool as pv to monitor the progress of our file transfer from either or both ends. These are only the updates that immediately present themselves, and there are sure to be quite a few others we come up with a little thought. Although we could access this functionality by using ready-made tools, such as Secure Shell (SSH), to provide this functionality, it is often a good thing when we can improvise what we need out of the materials we might have at hand.

# Nmap

As we discussed earlier in the chapter, we can make use of NSE to extend the capabilities of Nmap. In this section we will discuss the Lua programming language, in which NSE scripts are written, as well as some specific examples of what we can do with Nmap.

# Working With Service Probes in Nmap

One of the handy things we can do with Nmap is to probe for services on our target hosts. This allows us to add custom service definitions to Nmap, so we can detect running services outside the default list, specified in the nmap-service file, which is located in /usr/share/nmap on Kali. The nmap-service file is used to perform a simple match against the port number, and provides us with the name of the service that typically runs on port. When we run a default Nmap scan like nmap 10.0.0.51 with no options, the nmap-service file is used to provide the service information, as such:

```
PORT STATE SERVICE
80/tcp open http
139/tcp open netbios-ssn
9100/tcp open jetdirect
9101/tcp open jetdirect
9102/tcp open jetdirect
9110/tcp open unknown
9220/tcp open unknown
9290/tcp open unknown
```

As we said, this is simply a match from the nmap-service file, with no checks made. We can certainly edit this file to add or change entries, but this has limited utility as the file is exhaustive.

If we want to get a better idea of what exactly the running services are, we can run nmap -sV 10.0.0.51, which with the version checking turned on, should produce results along the lines of the following:

```
PORT STATE SERVICE VERSION
80/tcp open http Virata-EmWeb 6.1 (HP PhotoSmart/Desjet http config)
139/tcp open netbios-ssn?
9100/tcp open jetdirect?
9101/tcp open jetdirect?
9102/tcp open jetdirect?
9110/tcp open unknown
9220/tcp open hp-gsq HP Generic Scan Gateway 1.0
9290/tcp open hp-gsq IEEE 1284.4 scant peripheral gateway
```

service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at http://www.insecure.org/cgi-bin/servicefp-submit.cgi :
SF-Port9110-TCP:V=5.51%D=4/20%4Time=4DD72E40P=x\x86_64-unknown-linux-gnu

```
SF:%&r(RPCCck,2B,"\0)
(r\xfe\xid\x13\x01\x00\x01\x00\x00\x02\x00\x01\x86\x80\x0
SF:\x01\x91\x97\x00\x00\x00\x00\x00\x00\x00\x00
```

We can see here that we got back a bit more detailed information on several of the ports, although not everything was successful. This information is pulled from the entries in the nmap-
