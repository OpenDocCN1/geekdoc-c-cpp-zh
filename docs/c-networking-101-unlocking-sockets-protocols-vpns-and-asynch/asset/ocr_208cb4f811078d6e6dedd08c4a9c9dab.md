# Using Netstat

The netstat command (network statistics) is a command-line tool that displays network connections (both incoming and outgoing), routing tables, and a number of network interface and network protocol statistics. It is useful for checking your network's overall health, to find out how well your firewall is working, and for spotting suspicious network activity.

To use netstat, you open your command line interface and type netstat, possibly followed by some options. By default, it shows a list of active sockets for each protocol it supports. Now, let us look at a few examples:

# Example 1: Basic Netstat

In your terminal, type netstat. This will list all current network connections, along with protocol used, local and foreign addresses, and the state of the connection.

# Example 2: Displaying Only Listening Sockets