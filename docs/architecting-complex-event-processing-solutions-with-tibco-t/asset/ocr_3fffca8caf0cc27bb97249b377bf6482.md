recognition is the result of an analysis that determines something of business significance has occurred. Events that require this type of analysis are referred to as *complex events*.

# *Point and Interval Events*

Usually when you think about an event you associate the occurrence of the event with a point in time: the time at which the order was submitted or the time that the power failed. Generally, this is the time at which a technical event was captured. Such events are referred to as *point events*.

Some events, however, occur over a period of time. For example, the TIBCO User Conference (TUCON) is an event that takes place over several days. A television show happens over the course of 30 minutes or an hour. Events that occur over some period of time are *interval events*.

Why is this distinction important? It is important when you need to compare the temporal relationships between two events: Comparing interval events is more complicated than comparing point events. For a pair of point events, there are only three possible relationships: before, simultaneous, or after. For interval events, there are fifteen possible relationships between two events (Figure 2-2). The last two relationships are special cases in which one of the events has degenerated into a point event that is coincident with either the start or the end of the remaining interval.

# Missing Events

Sometimes the business-relevant event you are looking for is the observance that some other event was not observed, at least when it was expected. These cases arise when there is a service-level agreement regarding when an event should occur and the expected event does not occur within this time interval. Typically the beginning of this time interval coincides with some previous event: The clock marking the deadline for delivering a product starts when the order is placed.

Sometimes the recognition is more complicated: An event is supposed to occur at some regular intervals, and the observance is that the expected events have been absent for some period of time. This is a common approach to liveness testing: A component sends a heartbeat at regular intervals indicating that it is operating properly. The absence of these heartbeats for some period of time is an indication that there is a problem.