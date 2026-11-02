
## Chapter 12

## Using Existing Products

“Next item,” said Marcus. They were back in the old drawing office area, and had spent some hours working their way through a technical audit report. This audit had been one of the results of the ongoing negotiations with Factotum, and most of its concerns were about resilience.

“Recommendation 27b identifies problems of consistency between the instances of repair orders that are duplicated in different service centres,” Eleanor read from the pink sheet in front of her. “They are right; there is potentially a problem here, but it means adding transactional controls to all the order update steps. It will be a huge job, particularly when taken together with the improvements to archiving and disaster recovery we talked about before coffee.”

“What about replication transparency? That worked well for the logistics service, as I remember,” said Nigel, hopefully.

“Maybe,” Eleanor looked out, for a moment, over the cubicles on the floor below. “But I don’t think so; we would still need to factor in the channels to archival, and linking that whole subsystem with replication would be too damaging to performance.”

“Just explain that to me again, will you,” broke in Marcus, looking puzzled. “I thought transparencies hid all that sort of thing.”

“They hide complexity from the programmer, but the problem here is the real runtime costs of coordinating a larger number of objects. In any case, what we want from archival is resilience, which means keeping the boundary to it as clean as possible.” There was another pause.

“We could try a different approach,” said Alex, quietly. “If we don’t want the complexity of all these archive-based resilience mechanisms, can’t we avoid them completely?”

“But we spent half the morning identifying reasons why we must have them,” snapped Claire.

“Not quite. We have shown that we need consistency and resilience, not that we need to implement all those horrid mechanisms ourselves.”

“So what’s the alternative?”

“Don’t build the subsystem; buy what you want as a service. There have been a lot of developments recently in cloud computing. You could buy resilient, consistent storage from one of the global suppliers and use it as a secure mailbox between the local centres. That way the external supplier has to worry about the coordination and the disaster recovery. You agree on a suitable SLA with them, and they already have all the resources needed to provide it. All you have to worry about is the local centre access, and you can still use the replication transparency dodge to avoid visible complexity there.”

“OK,” said Marcus, “what’s the downside?”

“You have to allow for the risk and the recurrent cost. Costs shouldn’t be too far from a realistic total cost of ownership for the in-house solution, and may well be cheaper. There are always hidden costs you miss when assessing doing a job in-house. Risks are more difficult. You have to plan for commercial failure of your supplier, but they are a big player. You should look at a lower quality fallback system in the local centres and set up a commercial hedge.”

“You mean betting on the commercial failure of the biggest bookseller on the planet?” asked Ira. “This is serious dealing.”

“Indeed, but it has to be considered. More important, I think, are the risks to security, confidentiality and loss of control it implies. Do you trust your supplier to maintain a really stable service offering without changes in the specification? There is always the risk of over-enthusiastic upgrade.”

“Surely upgrades are safe?” Marcus looked puzzled again. “Improving a service can’t be a problem, can it?”

“Oh yes it can,” said Eleanor, ruefully, “Remember that online sales tax system a couple of years ago? We had just got it nicely bedded down when they upgraded it and added a whole extra level in their data model. It took weeks to get the miscodings out of our financial data and the internal audit people still remember all the special reconciliations.”

“OK, I remember that, but the idea still sounds interesting. Let’s talk about the detail.”

### 12.1 What Does This Product Do for Me?

One of the practical problems in using an architectural framework like ODP is that the world is seldom as simple as the textbooks assume. The picture of development taking place in isolation, from requirements to deployment, is far from reality. Rarely can a design team produce the specification of a complete enterprise system as a self-contained activity. Usually, they identify at least some components that are available elsewhere. The incorporation of commercial off-the-shelf products (COTS subsystems) shows the clearest separation of design responsibility and gives the best illustration of the issues. However, use of legacy components involves the same problems.

In essence, the problem to be solved arises from the need to retain the advantages of a clean architectural approach while incorporating subsystems that have already been produced, outside your control, and based on a different framework, or even with no clear framework at all. To be specific, how can components from a non-ODP culture be incorporated into our ODP world?

When you purchase a COTS product to perform some function, you surrender control of the detailed design. On the other hand, you get a working solution immediately and benefit from the supplier’s economies of scale. Or at least, you do if you select a well-established, reputable supplier. You also get ongoing support, maintenance and periodic upgrades. However, such upgrades can be a mixed blessing because they may introduce changes that invalidate the way you have integrated the product into your system.

There is certainly no magic bullet in this area. The customer wants guarantees of product stability from the supplier, but the supplier has to balance the conflicting demands that many different customers place upon them. They also need to innovate to attract new customers. The balance between these conflicting requirements will depend on the nature of the supplier’s business. A supplier who uses a family of components to offer individually tailored, bespoke solutions to respond to individual invitations to tender from their customers will be more likely to take account of individual customer constraints than one selling a generic product in shrink-wrapped form to thousands or even millions of customers.

A lot depends on the way the suppliers document their products, and how seriously they take the maintenance of this documentation, on the provision of advanced warnings of changes in the product and on the supply of transition tools to make the customer’s life easier. At the core of these documentation issues is the need to create suitable models, both of the product and of the way it is to be used; these models themselves need to be positioned within the ODP framework.

### 12.2 Supplier and User Views

The supplier will have its own specifications used in designing and constructing the product, but these include much private detail, so we concentrate here on a set of models related to its use. These have a number of jobs to do.

In an ideal world, the process of assessing the available products and deciding which to use will involve confirming the relationships between these various models (as well as many other factors involving value for money and commercial credibility, of course). We illustrate these relations in Figures 12.1 and 12.2, by showing the observable behaviour as Venn diagrams, so that subsets of possible behaviour are shown as included within their supersets. A product is suitable if the services it offers are a superset of those the user requires, and if the infrastructure support available in the user’s environment is a superset of the product’s requirements.

First, let us consider the infrastructure. The supplier will have a model, in functional terms, that describes the infrastructure needed to support the product; this model will, in general, describe several alternatives because it will cover a range of different environments in which the product can be deployed.
