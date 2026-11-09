data at times dictated by that schedule, and do something useful with the results of that analysis.

We’ll use report generation as a canonical example and set one up for our chat service: we’ll generate a report of how many messages per day were sent in each chat room.

# The Cron Scheduler

Our application has a file for a schedule. In Java, that file is named WEB-INF/cron.xml; in Python, it’s cron.yaml. Since we’re using the Java version of our chat app, we’ll put an entry into the WEB-INF/cron.xml file. That file contains a list of entries wrapped in an `<cronentries>` tag. Each entry is a `<cron>` element.

The cron entry contains three fields, represented as XML sub-elements:

<url>

First, it has a URL. As we’ve seen over and over in App Engine, it basically wraps everything in HTTP requests—pretty much everything is implemented using HTTP request handlers. Cron is no exception. App Engine will generate a **GET** request for this URL according to the schedule.

<description>

Next, there’s a description. This is just documentation; it has no execution-time effect. It’s there to let someone reading the cron file understand what the task is about.

<schedule>

A textual description of when the task should be invoked.

The schedule is written in what looks like an English description:

+   - *every number units*
+     Run at a specified interval. For example, every 2 hours, or every 3 minutes.
+   
+   - *every time*
+     Run at a specified time. For example, every monday 12:00 will run at noon on Mondays; or every day 00:00 will run every day at midnight.
+   
+   - *nth time of month*
+     To run your report less often, you can specify relative to months: 2nd tuesday (leaving out the month to mean *every month*), or 3rd friday of march,june,september,december to run the report four times a year.