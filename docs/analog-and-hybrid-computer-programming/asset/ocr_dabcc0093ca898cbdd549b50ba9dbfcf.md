![](bbox=[0.22, 0.12, 0.78, 0.32])

Fig. 5.35. Delaying a time-varying function

below) that have to be taken into account in an actual simulation setup. Delays of the first or second class are often preferred despite their shortcomings.

# 5.15.1 Historic approaches to delay

In the early days of analog computation an obvious way of implementing a delay was to use a magnetic tape drive. An adjustable time delay could be implemented by either varying the tape-speed or the distance between a pair of write and read heads. Apart from the high initial cost of the tape drive itself the required frequency modulators and demodulators feeding the write heads and driven by the read heads were extremely expensive and accordingly only a few installations could afford to employ this technique.58

Another much simpler classical approach is based on a so-called capacitor wheel which is an extension of today's sample and hold circuits. It basically consists of a large number of storage capacitors which are selected by motor-driven switches as shown in figure 5.36. Here the switches labelled 1 and 2 are driven in synchronism by a single shaft while the actual time delay is controlled by the switch labelled 3. This setup clearly belongs to the second class of delay circuits with continuous value representation but operating in discrete time. Its modern equivalent is the bucket brigade device, described in section 5.15.3.

The following sections will discuss the three basic classes of delay circuits and provide some practical implementation examples which are suitable for modern high-speed analog computers.