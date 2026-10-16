
Occasionally, we also come across perfective maintenance where quality and performance of the software is improved. Perfective maintenance tasks are product and process improvement projects. IEEE standard defines perfective maintenance as “modification of a software product after delivery to improve performance or maintainability.” It is now widely believed that software reliability enhancement is a social responsibility; it makes life safer. To fulfill these social expectations, responsible maintenance organizations gather such metrics. These are product and process performance metrics. Such metrics have rather complex definitions and are often based on mathematical models.

Corrective maintenance dominates the scenarios in some maintenance organizations. Some take up pure enhancements. In several other organizations, the three types coexist in a 3:1:1 ratio according to a study made by NC State University [2]. The ratio could be 1:3:1 in certain business contracts where the focus is on bug fixing. NC State University also mentions that corrective maintenance—the quick fixes—come in two styles: without document changes and with document changes in the 2:1 ratio.

In huge system enhancement contracts, such as in aerospace, a large number (thousands) of change requests are clubbed into a development package, and it goes through a full development life cycle for many years. Multiple variants of the product are released periodically. This becomes more complex than regular green field development projects. Additional activities such as impact analysis and regression testing are included to ensure that system integrity is maintained. For these projects, the metric approaches suggested in Chapter 6 are relevant and may be followed.

In maintenance projects, many data are collected by automated tools. However, the construction of metrics and models seems to be more difficult in maintenance projects than that in development projects. Maintenance tasks are shorter, and there is no time for manual data collection. Tool-collected data go into a database (“write-only” data base, Humphrey quipped) and is revisited by analysts who prepare reports for management and customers. Data, much less metrics, are not that visible to support teams.

Extraction of metrics from the database is performed based on the purpose at hand. The purpose could be weekly management reports or occasional construction of performance models.

Let us take a look at some typical maintenance metrics.

## BOX 7.1 SHOULD MAINTENANCE TEAM MEASURE SOFTWARE RELIABILITY?

Reliability is a product metric and is often considered as a development metric. However, the role of reliability assurance shifts with time, from the development team to the maintenance team. Under maintenance tasks, reliability can either grow or deteriorate. Many support teams do not measure reliability unless the contract demands such a metric. As software evolves during maintenance, entropy sets in and quality gradually diminishes.

> As a system evolves its complexity increases unless work is done to maintain or reduce it; the quality of such systems will appear to be declining unless they are rigorously maintained and adapted to operational environment changes.
> 
> Lehman’s Laws of Software Evolution

> It is becoming an implied need that the support teams look after software reliability too and hence must measure reliability.

## Maintainability Index

A code is maintainable if it is understandable, modifiable, and testable, three factors identified by Syvasya [3]. A simple rule is

> The more complex a code turns, the less maintainable it becomes.

A widely used and practical working metric, maintainability index, is defined as follows:

MI = 171 - 5.2lnV - 0.23G - 16.2lnLOC

where MI is the maintainability index, V is the Halstead volume, G is the cyclomatic complexity, and LOC is the count of source lines of code (SLOC).

Way back during coding, this metric could be used by a programmer to simplify a code in a systematic and measurable manner. The same metric can be used by the maintenance team to assess the application under maintenance. During the series of enhancements and feature additions, care may be taken to sustain high maintainability or even improve maintainability in preventive maintenance. This metric plays a fundamental role in the phases, coding, and maintenance:

> What is measured, improves.

Tracking this metric, during evolution of software during maintenance, helps to regulate and guide maintenance efforts.

## Change Requests Count

At the outset, the software size grows following an evolutionary path, release followed by release. Only a part of the software is not modified, as suggested by Lehman et al.

![](img/2f042205c6c0e14747f198ed8f9c9f40_125_0.png)

### Figure 7.1 Change request (CR) arrival.

[4], and shows an example: the total size of a system in modules and the part of the system not touched at each release are plotted as a function of release number. Both measures are expressed as a percentage of the largest size achieved by the system.

In this dynamic environment, maintenance teams have to respond to change requests from the field—from customers. Change requests need to be validated and analyzed, and fixes must be designed, built, tested, and finally released. The arrival of change requests from two applications under maintenance is shown in Figure 7.1.

Change requests from application 1 show a trend of growth, suggesting more changes in the months to come, whereas change requests from application 2 seem to have reached a plateau region, suggesting negligible number of changes in the months to come. Cumulative plots of change request counts are of immense value to the maintenance team. They indicate work done and predict work to be done. The metric is a direct count and does not involve complex calculations. Meaningful are the patterns discernible to the human eye.

## Customer Satisfaction Index

Measurement of customer satisfaction (CSAT) has a strong business purpose: it helps businesses grow. Maintenance metrics framework placed great emphasis on CSAT survey.

Customers take a more direct interest in bug fixing and tend to fill in customer satisfaction survey forms regularly and frequently. The factors selected for CSAT survey are unique and resemble typical sets used in the service industry. Zeithaml and Parasuraman’s [5] RATER model measures the following factors:

- Reliability
- Assurance
- Tangibles
- Empathy
- Responsiveness

More factors are added, and the previously mentioned factors are also tailored based on the business contract and customer’s special requirements.

Customer satisfaction against each factor is measured using the Likert scale. However, a continuous scale from 0 to 10 is simpler, more granular, and has advantages, presented as follows:

Undesirable 0 o—o—o—o—o—o—o—o—o—o—o 10 Excellent

The maintenance CSAT factors are very different from the factors used in development projects, and the priorities are different. Preferably, the factors should be selected in consultation with the customer to have a perfect alignment with customer’s expectations.

The CSAT index is a metric religiously collected in corrective maintenance operations; this is also the metrics more often seen by top management.

## Resource Utilization

There is always a mismatch between the volume of maintenance tasks and the available resources. Workload is not constant but fluctuates. Projects could be understaffed or resources could be idle.

Typical maintenance projects are run with minimal resources to reduce overhead costs; as a consequence, there is a backlog. However, the resource utilization metric will be reported as 100% every month. This metric is a fallacy unless it is seen in the context of performance and customer satisfaction. If there is overtime and if it is also recorded, human resources utilization will touch 120% and more, as has been occasionally reported in the industry. Such high scores are alarming; employees could be put under stress, and quality of work may be compromised. Fatigue affects the way the team members communicate and empathize with customers. The healthy range of this metric is between 95% and 98%.

Along with this metric, team skill index can also be measured using the data collection form shown in Figure 7.2. When the team skill index is low, it has two significant consequences: customer satisfaction falls low, and it takes longer to fix bugs.

## Service-Level Agreement Compliances

Service levels are specified in the maintenance contract. There are stringent specifications on the time to deliver each category of service. For example, the delivery time
