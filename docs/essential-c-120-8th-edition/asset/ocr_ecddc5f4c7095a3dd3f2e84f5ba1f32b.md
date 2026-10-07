# Chapter 15: Collection Interfaces with Standard Query Operators

# BEGINNER TOPIC

# Join Operations

Consider two collections of objects as shown in the Venn diagram in Figure 15.3. The left circle in the diagram includes all inventors, and the right circle contains all patents and patents. The intersection includes both inventors and patents, and a line is formed for each case where there is a match of inventors to patents. As the diagram shows, each inventor may have multiple patents and each patent can have one or more inventors. Each patent has an inventor, but in some cases, inventors do not yet have patents.

![](bbox=[0.125, 0.313, 0.816, 0.655])

FIGURE 15.3: Venn diagram of inventor and patent collections

Matching up inventors within the intersection to patents is an inner join. The result is a collection of inventor/patent pairs in which both patents and inventions exist for a pair. A left outer join includes all the items within the left circle regardless of whether they have a corresponding patent. In particular example, a right outer join would be the same as an inner join because there are no patents without inventors. Furthermore, the designation of left versus right is arbitrary, so there is really no distinction between left and outer joins. A full outer join, however,