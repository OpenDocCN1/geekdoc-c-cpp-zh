
## Innovation in Response

Analyzing events results in an understanding that a particular situation exists and a determination of what type of response, if any, is required. Innovation in response lies in improving the interaction between the party performing the analysis and the party executing the action. In all cases, requests (which are simply another form of event) must be sent to the party doing the work. However, there are two choices that impact the timeliness of the work performance. One choice lies in the delivery of the requests: Requests may be sent immediately, or they may accumulate and be sent periodically. The other choice lies in the timeliness of work performance: Work may be performed immediately upon request, or it may be performed at some later time.

Delays in work performance can negate any advantage gained in anticipating a situation. This is not to say that all work must be performed immediately, but rather that the timing of the work performance must be appropriate for the present situation.

In summary, there are two possible innovations in response. One is sending work requests immediately as soon as the need for the work is recognized. The other is in performing the work either immediately or within a timeframe appropriate to take advantage of a recognized situation. Together, these innovations enable the enterprise to respond more appropriately.

## The Event-Enabled Enterprise

From a business perspective, innovations in sensing, analyzing, and responding enable the enterprise to not only react faster and more appropriately to situations, but also to be proactive, anticipating situations and taking advantage of that anticipation. Both enable the enterprise to increase the value they deliver to their customers and business partners and gain competitive advantage. Realizing this business value requires the automation of sense, analysis, and response activities along with the appropriate positioning of reference information for immediate and efficient use.

So what is an event-enabled enterprise? It is simply an enterprise that has the infrastructure in place to sense, analyze, and respond to events as they occur and has positioned reference information to support this real-time activity. The event-enabled enterprise is thus in a position to efficiently innovate in how it senses, analyzes, and responds to the world around it. Through continuous innovation in these areas, the event-enabled enterprise distinguishes itself from its competitors and builds competitive advantage. Done well, such innovations provide extreme value for its customers, turning them into loyal fans.

## Summary

Extreme value sets your enterprise apart from its peers and turns your customers into loyal fans. Business process improvements are one way of providing this extreme value. These improvements make your enterprise more responsive to its customer base by innovations in how the enterprise senses, analyzes, and responds to the world around it. The most significant innovation lies in performing these activities in real time. Proactively sensing events—recognizing that something has happened rather than passively waiting to be told—is a significant enabler for this type of process improvement. The event-enabled enterprise is one that recognizes such events and continuously innovates in its analysis and response. It delivers extreme value to its customers.

## Chapter 2

### Concepts

### Objectives

The event-enabled enterprise concept is, itself, built upon a number of ideas. As a prerequisite to having a meaningful discussion about realizing the event-enabled enterprise, these underlying concepts must first be clearly understood. That is the purpose of this chapter.

After reading this chapter you will understand the essential concepts underlying the event-enabled enterprise: events, complex events, complex-event processing, context, event responses, and event-driven processes.

### Overview

The event-enabled enterprise (Figure 2-1) innovates in the manner in which it senses, analyzes, and responds to the world around it. It senses events that are happening in the world. When it senses an event occurring outside the enterprise, it announces the fact within the enterprise. This announcement becomes an internal event within the enterprise. The announcement triggers an analysis of the event, determining its business significance and whether a business response is required. The announcement that a response is required is another event, one that triggers the actual response. The response is an action, and the

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_38_0.png)

Figure 2-1: Event-Enabled Enterprise

completion of this action is, itself, an event—one that may be observable outside the enterprise. This is the way an event-enabled enterprise works.

### Events

An event is simply something that occurs: an order is placed, a service is delivered, a customer arrives on premises. To act on the event, you need to know what occurred and perhaps when it occurred, but first and foremost you need to recognize that it happened. The question is, how?

### Recognizing Events

On the surface, recognizing an event may appear trivial: The customer placed an order. But dig a bit deeper and some challenges appear. What if you are using a commercial off-the-shelf (COTS) software package to manage your orders? The event you seek is internal to the software package, an update to the database that underlies the system. What if the system does not provide a mechanism—a callback—to inform other components that an order has been placed?

In cases like this you must identify a mechanism for recognizing such events. There are a number of standard techniques for doing this. These techniques and their implementations are discussed in the companion book TIBCO® Architecture Fundamentals.¹

newly observable events. The eventual cost savings from improving the management of the service restoration process more than covers the cost of this work.

## Simple Event Recognition May Be Inadequate

Sometimes the business significant situation you are trying to recognize doesn’t correspond to a single event that can be observed. If you are looking for potential fraud on an account, a single failed login may not be significant: Users frequently make mistakes entering their userids and passwords. What is significant is that there have been repeated failed login attempts within a short period of time: for example, three failed logins in five minutes. In order to recognize the business-significant situation, the present event (the latest failed login attempt) must be correlated with earlier failed-login events. Events that require some kind of analysis in order to recognize an event of business significance are called complex events, a topic that will be discussed in more detail shortly.

## Categories of Events

Events can be categorized in a number of ways. These categorizations often impact the approach you will use to sense, analyze, and respond to the events, so these must be kept in mind as you conceptualize your solutions.

### *Technical and Business Events*

Events that can be directly observed are called *technical events*. Typically what is detected is a state change (e.g., a database update) in an application or a communication between components. *Business events* represent occurrences that are of business significance. But there is not always a 1:1 correspondence between technical and business events.

Some technical events represent occurrences that are of business significance, others (in fact, the majority of technical events) do not. Every click on every link on a website and every message being sent between systems is an occurrence that can be observed. However, only a subset of these technical events will likely be of business significance.

### *Simple and Complex Events*

A *simple event* is a business event that is also a technical event. But some business events don’t correspond to a single technical event: Their
