
Penny Wong stated that, “We accept the science and the advice that putting a price on carbon is the best way to reduce emissions.” This action sets up the environment for a transformation of the electricity supply sector in Australia. According to an article in *Climate Spectator* online on December 7, 2011:

> The government’s clean energy policy is currently centred around two basic principles—the 20 per cent [large-scale] renewable energy target (LRET) is designed to deploy the cheapest available renewable technologies, while the Clean Energy Finance Corporation will support the commercialization and deployment of those technologies that are likely to be the cheapest and the most useful in the future.

The LRET requires that by 2020, 20% of electricity will be supplied from renewable sources. This can be done in an ad hoc fashion, as is the present situation, with wind farms dominating large-scale installations and an intensification of photovoltaic installations on domestic houses (so much so that in NSW, for example, there is 300 megawatts (MW) installed). This is widely purported to be driving up the costs of electricity for the remainder of the population. However, this conjecture is disputed by the Australian Energy Market Commission, who estimate that the combined costs of feed-in tariffs and renewable energy schemes will make up about 14% of future price increases, whereas the cost of reinforcing transmission and distribution systems to cope with growth in peak demand will make up 49% of electricity price rises over the next 3 years’ [3]. To maximize greenhouse gas reduction, a more coordinated approach is necessary.

Maximizing the penetration of renewable energy sources for supplying electricity can be achieved through two disparate techniques: (1) building a supergrid, or (2) mixing the renewable sources with demand management and storage. In Europe, for example, there are proposals such as the Desertec initiative to create a supergrid interconnecting installations of renewable generation across Europe, North Africa, and the Middle East [21]. The underlying principle is that if you have solar farms distributed east-west along a latitude, there is an elongation of the solar day for providing energy for the grid. In addition, wind farms distributed north-south along a longitude can take advantage of weather systems moving cohesively at different latitudes. This concept of using meteorological and astronomical attributes to enhance the diversity of sources requires significant augmentation of the grid, including provision of high-voltage, direct-current transmission systems to minimize distance-related losses. In this configuration, even augmented by other renewable sources, there is a necessity for some energy storage for backup and load balancing—Denmark stores excess wind power in Norway’s hydroelectric dams through pumping.

Another challenge for today’s grid is the growth in air-conditioning penetration. In Western Sydney, more than 80% of homes now have air conditioning. This growth is driving energy supplies such as Ingleburn to spend approximately $3 billion over the next 5 years on grid infrastructure to meet the increased peak loads. But this extra infrastructure will only be needed for a few days a year; it’s like building a twenty-seven-lane freeway so that we never have peak-hour traffic jams.—*The Climate Spectator*, 14 July 2010.

An alternative approach is to develop a protocol for combining a renewable supply of diverse sources (both in technologies and locations) with sophisticated demand management (load follows the supply rather than the reverse) and energy storage to maximize the penetration of renewables. This entails a variety of supply options, more directly embedded in the transmission and distribution networks than the supergrid option, as well as a variety of storage options. The task arising from this more subtle approach is deciding on the quantities of each supply option, as well as a storage option, where they are positioned in the system, as well as how to best use the demand-side management. This results in a portfolio optimization problem.

In summary, in this chapter we present the mathematical modeling tools we argue are necessary to perform a rational, sophisticated analysis of the problem of moving to a high penetration of renewable sources in the provision of the electricity supply.

## 8.2 APPROACH

### 8.2.1 Renewable Generation

There are many renewable energy technologies that can generate electricity without consuming finite resources and without producing CO₂ emissions, including concentrating solar thermal plants, solar photovoltaic panels, wind turbines, tidal generators, and biofuel generators.

Zero Carbon Australia [41] describes an ambitious plan to meet Australia’s electricity needs using a combination of 60% concentrating solar thermal power (with molten salt storage), 40% wind, and backup power from hydroelectricity and biofuels. Elliston et al. [13] have shown that it is technically feasible to supply electricity from renewables with the same reliability as the present system.

### 8.2.2 Storage

- Short-term storage in electric vehicles
- Seasonal heat storage.

Many of these technologies have been demonstrated in medium- to large-scale installations. The problem is to develop methods that can determine which combination of storage technologies and locations will be most effective for a given electricity system.

### 8.2.3 Demand Management

The current electricity system is designed to supply whatever power is demanded, with little or no coordination of loads. As a result, the system is sized for peak demands that occur for only a few hours each year. The mean demand for power in the Australian National Electricity Market is 70% of the peak demand; in South Australia, the mean demand is just 50% of the peak demand. Figure 8.2 shows hourly demand for power in the National Electricity Market for each day of 2010.

Appliances are becoming more efficient, but we are using more of them. Increases in peak demand require upgrades to the transmission and distribution infrastructure, which adds significantly to the cost of electricity. Furthermore, fixed retail prices isolate residential and commercial consumers from supply constraints and the associated variations in generation costs. This problem can be partly addressed by time-of-use pricing, where electricity is cheaper during periods when demand is usually low; or by critical peak pricing, where the price to consumers varies with the cost of supply. An energy price that increases with power use would also encourage load leveling.

![](img/644775a10ad87164013616d709050cee_269_0.png)

FIGURE 8.2 (See color insert.) Hourly demand profile in the NEM for 2010 (data from Australian Energy Market Operator [5]).

Ultimately, however, we need appliances to respond to changing grid conditions to prevent overload. Demand management can defer the need for grid reinforcement, reduce the need for expensive generation used only during periods of high demand, and improve the quality and reliability of supply.

There is another important reason for demand management. As more energy is supplied from variable renewable energy sources, we will need to move from a system where supply follows demand to a system where demand also responds to variations in the available supply.

Over half of Australia’s electricity is used in the domestic and commercial sectors. Many domestic and commercial loads—air conditioning, water heaters, clothes and dishwashers, clothes dryers, refrigerators, freezers, pool pumps, and electric vehicle chargers—could be automatically rescheduled, to varying extents, without causing inconvenience. Australian Standard AS 4755 is defining a simple interface that will allow appliances to be controlled. Home Area Networks, Building Management Systems, and Smart Grids will also allow appliances and buildings to change their power demand in response to signals, including the price of electricity and the availability of renewable power. Still needed, however, are mechanisms that will encourage participation and allow smart appliances to fairly share the power available at any instant.

### 8.2.4 Mechanism Design for Demand Management

Mechanism design is a branch of mathematical game theory that seeks to design the rules of a game, for self-interested players with private information, to achieve an overall desirable outcome. One must design mechanisms that allocate available power to appliances in such a way that, when feasible, each appliance will complete its task on time. Allocation mechanisms should be “incentive compatible” so that players cannot gain by misreporting their requirements. When it is not possible to complete all tasks on time, mechanisms should allocate power as fairly as possible.

The 2007 Nobel Prize for Economic Sciences was awarded to Hurwicz, Maskin, and Myerson for their work on mechanism design theory. A report from the Royal Swedish Academy of Sciences [35] gives a good overview of the topic, as does Nisan et al. [28].

A group at the University of Southampton is currently investigating the use of mechanism design for demand-side management, demand aggregation, and for pricing electric vehicle charging [19, 32, 33]. Gerding
