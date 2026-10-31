
Event responses are generally determined by business rules. Sometimes the rules are not obvious because they are embedded in established practices. In such cases some effort will be required to understand and extract the business rules in preparation for re-implementing them as part of your solution. In other cases the business rules may be codified in well-defined formulas, decision trees, or decision tables ready for incorporation into the solution.

An event response in a CEP solution has a structure similar to that of an event analysis (Figure 2-8). The arrival of an event indicating that some situation exists (which could be either simple or complex) triggers an analysis to determine what the appropriate response should be for this situation. That analysis generally requires some contextual information. The results of the analysis are the events that trigger actions—the enterprise responses to the triggering event.

A trivial example is a business rule that says if the order amount exceeds $500, then an approval is required. The triggering event is the arrival of the order. The analysis is simply a comparison of the order amount with the threshold value. Depending upon your design decisions, the threshold value itself may be fixed in the analysis logic or it may be a piece of contextual information. The action is to initiate the approval process if required.

Trivial as this example is, it does raise an interesting design question with respect to the approval: To what extent should the component doing the response analysis also be responsible for ensuring that the follow-on approval activity is performed? Deciding which component is responsible is an important question for the solution as a whole, as the answer will impact the robustness of the solution.

A richer example is a business rule stating that unless 99% of the received data is valid, the data should be rejected. Here the triggering event is the arrival of the data. However, validating the data will likely require a lot of contextual information and a detailed statement of the validation rules. Even the response rules may be complicated. If the data does not meet the criteria, then clearly the data should be rejected; but if the data does meet the criteria, then the normal processing should be initiated. Again, the question of the CEP component’s role in monitoring this subsequent processing must be considered.

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_53_0.png)

**Figure 2-8:** *Event Response*

3. For an in-depth discussion of the design pattern choices and their impact on the overall solution robustness, see *TIBCO® Architecture Fundamentals*.

In the previous discussion, the tacit assumption has been that the information necessary to perform the validation is simply present as part of the context. But what if validation involves the invocation of services that perform some parts of the validation? Now the analysis takes on the flavor of orchestrating the services of other components, at least for part of the validation. The approach for performing this type of orchestration is a bit different and is described in Chapter 8.

## Event-Driven Processes

Events, and the ability to trigger activity based on the receipt of an event, make possible the implementation of an event-driven process as opposed to a request-driven process.

In a request-driven process (Figure 2-9), one party (party A in the figure) does two things: (1) recognizes that some condition has occurred, and (2) decides what action should be taken as a result and then initiates that action.

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_54_0.png)

**Figure 2-9:** *Request-Driven Process*

Figure 2-10 is an example of a request-driven process. Your car breaks down. You recognize that it is broken and decide to take the car to the repair shop. You ask the shop to fix your car. The shop diagnoses the problem and determines that your car requires some work for which it needs an authorization. It requests that you authorize the work. Once you have authorized the work, the shop recognizes that it requires parts and requests that the parts provider bring the parts. Once the repair has been completed, the shop requests that you pay for the service. Once you have paid, the repaired car is returned to you. This is the ultimate response to the initial request. This entire process is driven by requests.

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_55_0.png)

**Figure 2-10:** *Request-Driven Process Example*

In an event-driven process (Figure 2-11), the roles of recognizing a situation and of deciding what action to take are played by different parties. In the figure, party A recognizes that a particular condition exists and announces the existence of that condition. The announcement is an event. Party B responds to the event by determining the action that it considers appropriate and initiating that action.

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_56_0.png)

**Figure 2-11:** *Event-Driven Process*

This separation of responsibilities is the essence of an event-driven process and gives such processes their unique properties. Because recognition results in an announcement (an event), any party listening to that announcement can make an independent decision as to what action to take. This makes it possible to add, remove, or modify individual action decisions without impacting any of the other components. In contrast, in a request-driven process one party is making all the action decisions; any alterations require changes to that component.

Many event-driven processes are augmentations of request-driven processes. Figure 2-12 shows an event-driven fraud detection process augmenting a request-driven user login process. The figure shows the portions of the request-driven process related to the fraud detection. The hacker submits a login request. After checking to see whether the account is active (which it will be initially), the web site attempts to validate the credentials. If the login fails, the failed login screen is displayed and an announcement of the failed login is published. This is the trigger for the event-driven fraud detection process.

The failed login announcement is added to the record of recent logins being maintained in memory. The arrival of the new entry triggers an analysis to determine whether there have been three failed logins in the past five minutes. If so, a security alert (another event) is generated, and the account status is set to disabled. This action will impact the subsequent execution of the request-driven process: The next time the hacker tries to log in, the account-disabled screen will be displayed. The hacker won’t even get the opportunity to try another userid/password combination.

![](img/c5f9307fa62d0af5b0c26b57bacdb1b3_57_0.png)

**Figure 2-12:** *Event-Driven Process Example*

Of course, there are scenarios that have not been dealt with here that would be required in a real application. These would deal with issues such as re-enabling a user account and updating user credentials.

## Event-Enabled Enterprise Capabilities

The concepts discussed in this chapter provide a straightforward way to explain the capabilities of the event-enabled enterprise. The event-enabled enterprise is capable of the following:

- Recognizing and announcing events. This does not necessarily mean that every event is recognized and announced. It means that the enterprise has the infrastructure in place to recognize and raise the visibility of events as needed.
- Immediately analyzing and interpreting events in an appropriate context.
- Recognizing complex events.
- Performing context-dependent analysis to determine appropriate actions.
- Initiating required actions.

These capabilities make it possible for the event-enabled enterprise to innovate in the way it senses, analyzes, and responds to the world around it. Such innovations help it to build competitive advantage and turn customers into fans.

## Summary

Events are occurrences, things that happen. Technical events are those that can be directly observed. Business events are those whose recognition has business value. Some business events correspond to a single technical event.

Some events, known as complex events, are the result of an analysis that correlates one or more technical events with contextual information. The analysis determines whether something of business significance has occurred. Different parties may require different contextual information in order to determine the significance of the event.

This type of analysis, involving correlation and reference data, is referred to as complex-event processing. It can be applied both to recognizing situations and to determining appropriate responses.

Contextual information comes in many forms, including constants, reference data, and metadata. One of the significant challenges in complex-event processing is identifying the contextual information that will be required and ensuring its availability to support efficient real-time analysis.

When events drive processes, the result is an event-driven process as opposed to a request-driven process. In a request-driven process a single party both recognizes that a situation has occurred and determines what the response should be. In an event-driven process these two roles are separated, with one party recognizing the situation and
