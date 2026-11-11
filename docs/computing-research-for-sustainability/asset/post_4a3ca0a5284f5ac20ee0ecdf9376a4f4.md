
- How can large-scale science addressing real-world problems be made credible, if reproducibility is not possible?
- What lessons can be applied from the transformation of the Internet into a critical infrastructure that must avoid ossification?
- What is the appropriate mix of empiricism, innovation, and application in order for computer science to have an impact in the area of environmental sustainability?

## The Energy Challenge

Participants suggested considering broad sustainability challenges in the context of the energy challenge. The interconnected nature of people's basic resource needs, such as water, energy, and transportation, and the economic arrangements among these resources create a very complex problem. However, these interactions also mean that the energy challenge can serve as a useful proxy for sustainability challenges related to other limited resources.

The primary function of the electric grid is to deliver high-quality, low-cost power to millions of customers who are geographically distributed over thousands of miles. The fact that consumers have been able to make use of the grid without needing much knowledge about their own consumption patterns, or about where the power is coming from, has contributed to rapid economic and industrial growth. People have been able to use a comparatively inexpensive resource—energy created mostly through the burning of fossil fuels—essentially indiscriminately to expand the production of products that spur the economy. Additionally, enabling a usage model in which consumers could remain ignorant of their own consumption patterns meant that the grid has been tasked with delivering a high-quality commodity at extremely low cost. Moreover, the expectation has been that power would be delivered immediately as needed. The power grid is expected to meet these goals with minimal forecasting or anticipation of that need, except at very coarse granularity, and without inventory storage along the energy supply chain.

The current energy model is increasingly complex, with numerous sources of energy, a variety of stakeholders and consumers, and a not insignificant fraction lost during transport. A pressing sustainability challenge revolves around these questions: How can energy use be reduced, and can it be done without significant economic hardship? The following question was discussed: Where and how can computer science fit into this picture?

Figure A.4 shows the percentage of energy use in the United States by type. Each of these types represents an opportunity for reduction in demand. Commercial light use and residential heating make up the bulk of their respective building types, but several other smaller items make up the rest of the energy usage. Perhaps reductions in several of these “low-hanging fruit” items can contribute significantly in reducing total energy consumption.

![](img/c6a60667ee0f315137df705da9549366_155_0.png)

FIGURE A.4 Energy consumption in the United States, by type of use. SOURCE: Lawrence Berkeley National Laboratory.

## Impediments to Changing the Energy System

### Insufficient Scope and Scale of Research and Development

### Funding to Fuel IT-Enabled Innovation in the Electricity Sector

Challenged to consider opportunities for IT and CS research to contribute to sustainability, participants reflected on the history of IT successes and on whether those successes might offer important lessons. The enormous payoffs from IT R&D investment have been investigated by several studies of the National Research Council’s Computer Science and Telecommunications Board, including *Evolving the High Performance Computing and Communications Initiative to Support the Nation’s Infrastructure* (1995); *Funding a Revolution: Government Support for Computing Research* (1999); *Making IT Better: Expanding Information Technology Research to Meet Society's Needs* (2000); and *Innovation in Information Technology* (2003).²⁵ These reports have shown how research partnerships between the federal government and industry ultimately led to the creation of many well-known multibillion-dollar industries. These results suggest the potential sustainability payoffs from the right investments in IT.

Many of the advances presented in the CSTB reports, such as those in processors or networking, required significant financial investment from both industry and government. The software industry spends approximately 13.5 percent of revenues on R&D, the health care industry spends about the same, and the computer hardware industry spends about half of that.²⁶ By contrast, R&D spending by the electric utility sector is about 0.1 percent of revenues, perhaps due to the fact that the sector has been very stable, with little innovation or push for innovation, a context that seems to be changing rapidly.²⁷

Sustainability is a large, broad-ranging problem, and apportioning limited research dollars to effective ends is a difficult challenge. One consequence of this low level of support and the resulting small number of technical researchers at utility companies is that opportunities for partnership between academic researchers and utility companies are rare.

Government funding is also limited. In 2010, the U.S. Department of Energy provided $130 million and created three different energy hubs in innovation.²⁸ However, a workshop attendee commented that even this amount is much smaller than would be needed if a significant shift were to be made toward sustainable energy sources or if total energy consumption were to be decreased.

### Misalignment of Incentives for More Sustainable Generation and Use

The energy-utility market, as described earlier, has evolved to provide a critical resource, at low price, with supply almost instantaneously energy use is even more dispersed. Each industry that participates in the energy market has its own unique needs, regulatory requirements, and certification programs. Individual industries and companies create their own technology standards. Unique industry and corporate technology standards also make one-size-fits-all solutions impractical. Efforts to deploy, say, monitoring and data-collection tools in these sorts of environments are challenged. Equipment used for monitoring the use of each resource system—energy, water, food—within cities becomes difficult to build and deploy. Additionally, these monitoring devices, if built into the initial infrastructure, need to be able to collect a wide variety of data and be sturdy enough to function over long periods of time.

25 National Research Council, Evolving the High Performance Computing and Communications Initiative to Support the Nation's Infrastructure, Washington, D.C.: National Academy Press (1995); National Research Council, Funding a Revolution: Government Support for Computing Research, Washington, D.C.: National Academy Press (1999); National Research Council, Making IT Better: Expanding Information Technology Research to Meet Society's Needs, Washington, D.C.: National Academy Press (2000); National Research Council, Innovation in Information Technology, Washington, D.C.: The National Academies Press (2003).

26 Jill Jusko, R&D Spending: By the Numbers, Industryweek.com, January 2010. Available at http://www.industryweek.com/articles/rd_spending_by_the_numbers_17988.aspx.

27 Jusko, R&D Spending, 2010, available at http://www.industryweek.com/articles/rd_spending_by_the_numbers_17988.aspx.

28 Department of Energy, “Obama Administration Launches $130 Million Building Energy Efficiency Effort,” February 12, 2010, available at http://energy.gov/articles/obama-administration-launches-130-million-building-energy-efficiency-effort.

### Research Impediments

The critical nature of the sustainability problem and energy crisis combined with their scale and complexity often means that researchers are dedicating entire careers working to address pieces of the problem. This scale and complexity mean that choosing avenues of investigation is a high-risk proposition. If a path that a researcher follows turns out to be incorrect or a dead end, the mistake can be career ending. Furthermore, these sustainability and energy problems are inherently multidisciplinary, which adds another barrier to academic work often confined to single disciplines.

In many subfields of computer science, the ultimate goals can be defined reasonably clearly, even if the description of the goal is as simple as: Make computers faster. Well-defined goals also imply a clear definition of success. While there are some goals to work toward in addressing the sustainability problem, such as decreasing the levels of greenhouse gases in the atmosphere, they tend to be less well defined (should the focus be on lowering energy use or on the use of more sustainable energy sources?) and have less clear benchmarks for success.

## Potential Computer Science Contributions

In the fourth session of the workshop, participants brainstormed about potential further contributions of computer science to sustainability. Computer science is well positioned to provide technical options that could help address some sustainability challenges. Additionally, the distinctive culture, methodologies, and approaches of computer science may shed new light on methodologies, processes, and concepts that could be useful in sustainability. Speakers discussed several such cultural attributes, including the following:
