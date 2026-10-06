first character, and set the rkey and filename variables based on the null-separated values we expect. If the first character is something else, which our session should always be, we try to parse it like a data packet. We take the session as the first character up to the second null our packet is our packet number. The rest of the packet is our file data. We turn ses and pkt back into integers, and check to see if the information we had fewer than 1024 characters. If it did, that should be our last packet, as we have been making sure to send 1024 characters each time we send our UDP packets.

```
if type and rkey == @key
if type == @Write[0]
ses = Time.to_i
@sessions[ses] [:file] => rfile, :data => []
@sock.send("\001#[{}\000",0,sender.last,sender[1])
end
elsif ses and @sessions.has_key? ses.to_i
@sessions[ses][:pkt_to] = data
if last == 1
f = File.new(@sessions[ses][:file],"w")
f.puts(@sessions[ses][:data].join(""))
f.close
@sessions.delete(ses)
end
}
```

Now we have all the core information required to process our packet. So we determine if the type variable was set. If it was, and it was equal to write, we initialize a new session. Our session ID is the current time in integer format. This is not overly secure, but it is secure enough for what we are doing. We create a new session with our session ID and create a new hash to hold our filename and data. Our data will be stored in an array. This lets us store each packet in its own field numbered by the packet number. This lets us receive packets out of order and still put them back together. Once the session is initialized, we return the session information to the client so that the