produced from any Producer will be consumed by all Consumers?

# 22.2.4. Busses

A Bus is the PureScript Type that implements what’s known as a *Data Bus*, which is a data structure and associated API that facilitates data to be written by one or more Publishers. This data will be broadcast to one or more Subscribers, who will each get a copy of the data.

Busses can be read-only, write-only or read-write.

Let’s write a simple program that uses a Bus: