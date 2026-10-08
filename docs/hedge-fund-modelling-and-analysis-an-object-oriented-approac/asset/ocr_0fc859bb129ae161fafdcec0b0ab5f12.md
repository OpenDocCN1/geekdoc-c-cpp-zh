# CHAPTER 7

# # Market Risk Management

We have encountered throughout the book the problems relating to the risk that the value of a hedge fund will decrease due to the impact of various market factors, for example changes in interest and foreign currency rates. Moreover, with the heightened publicity of recent financial events, hedge funds have come under increased pressure from investors and regulators to efficiently manage, monitor, measure and report such risk inherent in their investment strategies. Indeed, experience has clearly shown that the measurement and management of extreme market conditions is of paramount importance for hedge funds.

Chapter 7 provides an introduction to market risk management for hedge funds and presents the fundamentals of quantitative risk measures and models used in the industry today. The chapter also covers some of the more advanced risk measures available that can more effectively manage risk in a hedge fund in light of the limitations encountered with traditional market risk measures.

# ### 7.1 THE RMetrics CLASS

In the previous chapters we will be developing a further class RMetrics in much the same as we did for the other classes. Source 7.1 shows the basic skeleton of the RMetrics class which we will add to as we develop through the chapter.

```
SOURCE 7.1: SKELETON OF THE RMetrics CLASS

// RMetrics.h
#pragma once;

#include "Utils.h"
```