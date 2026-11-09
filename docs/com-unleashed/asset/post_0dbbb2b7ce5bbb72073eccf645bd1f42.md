
**FIGURE 2.2**  
*A well-balanced application*

![](img/112c2326f49d26b8d59aa054e14c5747_59_0.png)

On the presentation side, this could mean adding data-aware or data-bound controls that talk directly to the data-access tier (see Figure 2.3).

**FIGURE 2.3**  
*Too much responsibility on the GUI.*

![](img/112c2326f49d26b8d59aa054e14c5747_59_1.png)

In turn, relying heavily on database-specific logic mechanisms like stored procedures or triggers on the data services tier will have the opposite effect, tipping the balance to the data services side (see Figure 2.4).

**FIGURE 2.4**  
*Too much responsibility on the server.*

![](img/112c2326f49d26b8d59aa054e14c5747_59_2.png)

Now consider Figure 2.5, in which a solid three-tiered design rests on an immovable foundation of logic that eliminates the fulcrum and the chance of disturbing the balance. A square represents a rigid foundation, unshaken by future upgrades or modifications to any tier.

![](img/112c2326f49d26b8d59aa054e14c5747_60_0.png)

This rigid foundation is achieved by the clear separation of presentation and data logic from the business rules. As long as the problems that the application is trying to solve are oblivious to where the data comes from (if any), or how it is presented, it will remain scalable and robust with time.

The three-tiered architecture is not just for client/server environments. Virtually all applications can be divided into at least three tiers as described. (As an exception, however, consider device drivers and other low-level hardware manipulation programs in which the extra three-tiered design effort can be counterproductive.)

Whether you are building a small Win32-based application or a full-blown, Web-enabled e-commerce system, the principles are applied equally. No matter how complex the problem, software always deals with data in some form (or there would be no work to do) and can always be separated by behavior into distinct layers.

## Multitiered Design

As applications evolve and become more complex, it is sometimes necessary to break one particular tier into two or more. This results in multitiered, or n-tiered, architectures. Although the fundamental interaction with a user might be the same (present data, gather data, and store data), it is sometimes easier to break the three basic tiers into several pieces.

For large complex applications with dozens of developers, it is much easier to work with an n-tiered architecture than a three-tiered one because the work can be carried out separately in finer granularity. COM+ assists in n-tier development because developers can create components that communicate across boundaries.

Consider Figure 2.6. This is an actual architecture diagram I used for a complex Web-based project. What once was the presentation tier in the three-tiered model has been broken into two independent tiers: Win32 and HTML.

**FIGURE 2.6**  
*A real-world n-tier architecture.*

![](img/112c2326f49d26b8d59aa054e14c5747_61_0.png)

When examining Figure 2.6, you might be asking yourself, “Why not keep one tier, as before, and two components that handle both HTML and Win32, respectively, adding interfaces and methods as required?” The answer is Win32 can be so complex that it would require a large set of homogenous Win32 components to coexist with another large set of homogenous HTML components. Win32 is inherently different from HTML processing (linear and event-driven instead of nonlinear and static).

As you might recall, a tier is defined as a collection of independent homogenous objects that work together to solve a common goal. By breaking down the tiers, and thus the number of components in each tier, you can greatly reduce the development and testing complexity of an application in a team environment. Independently developing and maintaining 5 components is much easier than doing so with 20.

The more components you have in a tier, the more the tier approaches a monolithic model (too much coupling), defeating the purpose of tiered architectures. In the case of HTML and Win32 as presentation choices, separating them into two tiers is a sound logical choice.

> **Note**
> 
> Do not confuse Figure 2.6 with a flow control diagram. It shows only the main problems of the application as abstracted in human terms. From this diagram, you cannot infer or assume communication interfaces or how data might flow throughout the application (uni- or bi-directional, concurrently, asynchronously, and so on).

> **Caution**
> 
> There must certainly be a threshold set in the minimum number of components a tier should contain. If you were to make each component its own tier, you would be back where you started (all components, no homogeneous organization). When architecting an application, use tiers to your advantage but be frugal in their quantity.

Moving down from the top presentation tiers are four separate tiers that would normally be contained in the business tier. By breaking them apart according to general functional goals, it is much easier to understand what the application is doing: validating data, crunching data, securing data (encryption, authentication, and so on), and transacting data. Each of these actions could certainly be contained in a single tier, but doing so would crowd the tier and render it unmanageable—a contradiction of the model’s main purpose.

Figure 2.7 shows a closer view on the Data Validation/Shaping tier. You can see it contains many different, but functionally similar, components. Each one solves a different problem within the validation domain of the application. Although validation can be considered a business-tier functionality, the validation components have little or no relation to crunching the data itself.

The next section talks about where your tiers should be physically placed in a deployment configuration.

**FIGURE 2.7**  
*Focusing on the Data Validation tier.*

**Data Validation/Shaping Tier**

![](img/112c2326f49d26b8d59aa054e14c5747_63_0.png)

## Local or Distributed?

Do not be fooled by the apparent distribution of the disconnected layers in a multilayered architecture. Programming with tiers does not imply a distributed relationship or even the presence of a database. It is a road map to follow and can be used for any application. Some applications do not even require a presentation layer. They might be services, for example, listening for non-interactive requests. Likewise, a data services tier can be absent if the application doesn’t involve persistence (like the calculator usually found under the Accessories menu in Windows).

## Good Design Techniques

Fortunately, sound design principles are very easy to apply to component-based software. You will not examine the more involved object-oriented approaches that exist, but instead will cover tried-and-true techniques for designing multitiered COM+ architectures. In order of importance, they are

- 1. Abstract the application into heterogeneous functional tiers.
- 2. Identify components to carry out finely grained behaviors.
- 3. Create interfaces or glue between the layers.
- 4. Implement the component interfaces and their methods.

From these techniques or principles, it is clear we are following an inductive approach. We start from the general and delve into the details.

### Abstract the Application into Tiers

All useful software is created to solve one or more problems. All problems can always be divided or separated into subproblems. With components, it is important to split large and sophisticated problems into smaller, more manageable ones. By using this divide-and-conquer approach, we ensure that the problem as a whole will be solved and also create a robust and easily maintainable architecture. It is much easier to modify and upgrade a single component consisting of a subproblem than to try to tackle an entire monolithic problem, with the usual retesting and debugging.

### Identify Components

This phase is a little more challenging and requires foresight (and hindsight). It’s probably the most fun and creative phase of all because it brings together past experiences, current technology, and analytical problem solving.

Again, although not all applications can seamlessly fit the three-tiered model, they can always be logically separated into this abstraction at some level.

Start with presentation. Will the application interact with a user via a graphic interface or is it a service that fulfills requests blindly? Creating intuitive and user-friendly GUIs is not a trivial task. All too often, you see GUIs that are plagued with inconsistencies from screen to screen or are too busy. This only compounds the problems when you are working with browsers and their lack of rich control sets or state.

You won’t learn GUI design here, but it is worth mentioning that it should not be taken lightly. Remember that although the presentation tier is just the tip of the iceberg, it is the one and only communication link between a user and what constitutes the application. The tiny presentation tier can be sitting on the shoulders of a huge sophisticated business tier, but if it’s not exporting a user-friendly working environment, or is inconsistent, the user might unfairly dismiss the entire application.

![](img/112c2326f49d26b8d59aa054e14c5747_64_0.png)
