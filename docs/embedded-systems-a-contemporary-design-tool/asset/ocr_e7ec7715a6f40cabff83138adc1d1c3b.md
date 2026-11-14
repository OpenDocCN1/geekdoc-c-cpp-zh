increased, so did the need for a more reliable means of affecting that exchange. In addition, as the telecommunications field started to grow, so did the number of vendors offering equipment – often with incompatible interfaces. As we will learn when we study the USB interface, these requirements and expectations drove the need for standardization. The standard that was adopted was the RS-232 interface. It specified signaling voltages, timing, and functions as well as a protocol for exchanging information, the physical connectors, and pin assignments for the equipment involved in the exchange. The specific equipment was a piece of DCE and a piece of DTE.

Since 1960, the standard has seen three modifications. In addition to the name change to EIA-232, several of the signals have been renamed and new ones have been added. The most current version of the standard is designated EIA-232E.

Its ease of use has led to such a plethora of variations that the original intent of the standard has become clouded or forgotten. Today these variations often appear under the name RS-232, but in use they take a significant departure from the original intent. As a result, significant amounts of time, money, and frustration are often spent trying to sort all this out. Before we look at how RS-232 is typically misused, let’s look at its initial intended purpose in a bit more detail.

# 18.3.2 The EIA-232 Standard

The EIA-232 standard specifies the signals and interconnecting lines between DTE and DCE devices. The full standard specifies that the DTE device uses a 25-pin DB25P (male) connector and the DCE end uses a mating 25 pin DB25S (female) connector. The standard specifies signals for 22 of the available pins. Today a subset of these appears on a wide variety of computing equipment, with cables terminating in DB9P and DB9S connectors. In either case, the original cabling is parallel, straight through – no crossover connections. The drawings in Figure 18.1 show the pin numbers on the DB-9 and DB-25 connectors as well as the EIA-232 inputs/outputs to which they correspond.

![](bbox=[0.13, 0.55, 0.72, 0.78])

Figure 18.1 Pin Numbering for the DB-9 and DB-25 EIA-232 Connectors

Figure 18.2 gives a high-level picture of a representative early communications system. Note, once again, that the RS-232 interface was strictly defined between a piece of DTE, a computer of one form or another, and a piece of DCE, typically a modem.