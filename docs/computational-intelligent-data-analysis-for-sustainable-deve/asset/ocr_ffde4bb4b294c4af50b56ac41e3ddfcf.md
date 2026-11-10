a diagonal band will be seen as value cascades from primary industries in the upper left to tertiary production industries in the lower right. For example, if the Wheat, Flour, Baking, and Retail Bakery sectors are adjacent in the classification system, then much of the output from each will directly be used as input into the next, forming a diagonal band in the table.

IO tables should be balanced. The sum of each row should equal the sum of each column. If an industry is not balanced, it means the industry is either receiving inputs from, or delivering outputs to, an unknown source. A significant challenge in assembling a large MRIO table has been to ensure this balancing. We discuss below how the Eora project uses an optimizer to ensure the table is balanced.

The Eora MRIO is available in five valuations: sales prices as recorded by sellers, the additional cost of taxes paid, the value of subsidies received, transportation costs, and retail and distribution costs. These margins allow distinction of the several types of middleman price markups between producers and purchasers. Taxes, subsidies, transportation, and retail and distribution costs are added to the producer’s price to arrive at the purchaser’s price. These markups are represented by four additional sheets on top of the basic price IO table (Figure 2.5). Separating these markups into separate sheets is useful for analyzing the effects of policy changes on taxes, subsidies, and transportation costs, and how these changes differentially affect sellers and purchasers.

Structurally, Eora is a tensor. In the most intuitive representation, it is a three-dimensional tensor: a vertical stack of five matrices. However, we address it as an eight-dimensional tensor. The rows and columns have a logical hierarchical grouping illustrated in Figure 2.6.

To quickly locate a particular element in the tensor, we use an eight-dimensional address of the form:

+   Input country/block/sector index
+   Output country/block/sector index
+   Sheet
+   Year

The two “block” dimensions group sectors as value-add sectors, final demand sectors, industries, commodities, or satellite (Q block) sectors. This eight-dimensional addressing is used in the AISHA (An Automated Integration System for Harmonised Accounts) data processing language to specify regions of the Eora tensor.