newly observable events. The eventual cost savings from improving the management of the service restoration process more than covers the cost of this work.

# Simple Event Recognition May Be Inadequate

Sometimes the business significant situation you are trying to recognize doesn’t correspond to a single event that can be observed. If you are looking for potential fraud on an account, a single failed login may not be significant: Users frequently make mistakes entering their userids and passwords. What is significant is that there have been repeated failed login attempts within a short period of time: for example, three failed logins in five minutes. In order to recognize the business-significant situation, the present event (the latest failed login attempt) must be correlated with earlier failed-login events. Events that require some kind of analysis in order to recognize an event of business significance are called complex events, a topic that will be discussed in more detail shortly.

# Categories of Events

Events can be categorized in a number of ways. These categorizations often impact the approach you will use to sense, analyze, and respond to the events, so these must be kept in mind as you conceptualize your solutions.

# *Technical and Business Events*

Events that can be directly observed are called *technical events*. Typically what is detected is a state change (e.g., a database update) in an application or a communication between components. *Business events* represent occurrences that are of business significance. But there is not always a 1:1 correspondence between technical and business events.

Some technical events represent occurrences that are of business significance, others (in fact, the majority of technical events) do not. Every click on every link on a website and every message being sent between systems is an occurrence that can be observed. However, only a subset of these technical events will likely be of business significance.

# *Simple and Complex Events*

A *simple event* is a business event that is also a technical event. But some business events don’t correspond to a single technical event: Their