By default, Powerpoint uses the *Normal view* for display as indicated by the first of the three icons at the bottom. The next icon represents the *Slide Sorter View* which displays the thumbnails of the slides. You can rearrange slides by simply dragging these thumbnails or using the cut-copy-paste facilities available on right-clicking each slide. The presentation can eventually be viewed by clicking on the third icon that represents *Slide Show*, or using the menu option at the top of the screen.

Besides containing formatted text, a slide can feature graphics, audio and video. Each slide can also have (i) *animation* which determines how the text is moved to the screen, (ii) *transition* which controls the way one slide vanishes and the next one appears. The quality of the overall presentation is enhanced by choosing a proper background for each slide.

# 2.13  UNDERSTANDING A TCP/IP NETWORK

We live in a connected world where computers talk to one another using networking protocols. A *protocol* is a set of rules used by two or more machines to communicate with one another. The standard protocols used on the Internet are collectively known as *TCP/IP*. The acronym expands to *Transmission Control Protocol/Internet Protocol*, but the name is somewhat of a misnomer because it is a collection of several protocols (of which TCP and IP are the most important ones). The Net is running on TCP/IP since 1983.

Unlike our fixed-line telephone system, TCP/IP is a *packet-switching* system. Data are broken into *packets* with the sender’s and recipient’s addresses written on them. As the packets travel along the network, they encounter routers which look at the addresses to determine the most efficient route a packet has to take to move *closer* to its destination. Packets may move along different routes and arrive out of order. They are reassembled in the correct order at the destination before they finally reach the application.

# 2.13.1  Hostnames and IP Addresses

In a network, a computer is known as a *host*, sometimes a *node*, and every such host has a *hostname*. Depending on whether a network is part of the Internet, a host in such a network could take on one of the following forms:

| Hostname | Description |
|---|---|
| `earth` | A hostname |
| `earth.planets.com` | A fully qualified domain name |

Every host in the network has an address, called the *IP address* which is used by other machines to communicate with it. This address is a series of four dot-delimited numbers (called *octets*) which could typically look like this:

```
92.168.0.1
```

The maximum value of each *octet* is 255. This address has to be unique not only within the network, but also in all connected networks. And, if the network is hooked up to the Internet, it has to be unique throughout the world. TCP/IP applications can address a host by its hostname as well as its IP address:

```
telnet earth
ftp 92.168.0.1
```