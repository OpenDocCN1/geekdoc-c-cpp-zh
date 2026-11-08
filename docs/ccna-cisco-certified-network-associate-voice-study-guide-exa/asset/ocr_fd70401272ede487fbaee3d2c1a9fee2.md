```
```c
if (collision detected by ...)
{
    count a third-party loop;
    abort processing of data packet or control element;
    /* MAY choose a different policy to keep new source */
}
/* A collision or loop of the participant's own packets */
else if (source transport address is found in the list of
         conflicting data or control source transport
         addresses) {
    /* OPTIONAL error counter step */
    if (source identifier is not from an RTCP SDES chunk
        containing a CNAME item or CNAME is the
        participant's own) {
        count occurrence of own traffic looped;
    }
    mark current time in conflicting address list entry;
    abort processing of data packet or control element;
}
/* New collision, change SSRC identifier */
else
{
    log occurrence of a collision;
    create a new entry in the conflicting data or control
    source transport address list and mark current time;
    send an RTCP BYE packet with the old SSRC identifier;
    choose a new SSRC identifier;
    create a new entry in the source identifier table with
    the old SSRC plus the source transport address from
    the data or control packet being processed;
}
```
```

Because RTP is used to transfer the data packets and provides no session setup or management, another protocol is needed for the monitoring of a data stream. This is where the RTCP protocol comes in.

# RTCP

The RTP Control Protocol (RTCP) is used to provide four basic functions. The first and primary function is providing feedback on the quality of data distribution. The information provided may be used for control of dynamic or adaptive encoding