![](bbox=[0.117, 0.085, 0.858, 0.497])

# FIGURE 2.5 Running webCheck.py using

OptionParser.

# Lists

Let's say we need to convert a Classless Inter-Domain Routing (CIDR)-formatted IP address into an IP range and netmask. CIDR format is a way to express information about an IP address. Instead of listing out the full network information, only the IP address and the number of bits in the netmask are present. There are a few ways to do this. We can calculate it by hand, use a subnet calculator, or write a script. Since you're reading a scripting book, we should probably use a script. This will also give us an opportunity to explore lists. Lists are Python's version of arrays. They are objects with their own methods. Let me make something like this:

```
root@bt:~ ./subcalc.py 192.168.1.1/24
```

First, we'll want to split the input (192.168.1.1/24) into the CIDR and