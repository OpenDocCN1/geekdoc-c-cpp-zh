Convert the semantic net shown in Figure 2.5 on page 65 to a series of facts in a defacts statement. Use several defemplates to describe the facts. For example, the IS-A and AKO links should be relation names and each should have their own deftemplate.

Convert the binary decision tree representing animal classification information in Figure 3.3 on page 99 to a series of facts in a defacts statement. Show how the links between the nodes can be represented. Do the leaves of the tree require a different representation from the other nodes of the tree?

Implement the semantic net of Problem 2.1 as a defacts statement using AKO and IS-A deftemplates.

Plants require many different types of nutrients for proper growth. Three of the most important plant nutrients that are provided by fertilizer are nitrogen, phosphorus, and potassium. A deficiency in one of these nutrients will produce various symptoms. Translate the heuristics below to rules that determine nutrient deficiency. Assume that the plant is normally green.

+   A plant with stunted growth may have a nitrogen deficiency.
+   A plant that is pale yellow in color may have a nitrogen deficiency.
+   A plant that has reddish-brown leaf edges may have a nitrogen deficiency.
+   A plant with stunted root growth may have a phosphorus deficiency.
+   A plant with spindly stalk may have a phosphorus deficiency.
+   A plant that is purplish in color may have a phosphorus deficiency.
+   A plant that has delayed in maturing may have a phosphorus deficiency.
+   A plant with leaf edges that appear scorched may have a potassium deficiency.
+   A plant with weakened stems may have a potassium deficiency.
+   A plant with shriveled seeds or fruits may have a potassium deficiency.

Use deftemplates to describe the facts used in the rules. The input to the program should be made by asserting symptoms as facts. The output should indicate which nutrient deficiencies exist by printing to the terminal. Implement a method so multiple printouts for a single deficiency caused by more than one symptom are avoided. Test your program with the following inputs:

+   The plant has stunted root growth.
+   The plant is purplish in color.

Fires are classified according to the principal burning material. Translate the following information to rules for determining fire class:

+   Type A fires involve ordinary combustibles such as paper, wood, and cloth.
+   Type B fires involve flammable and combustible liquids (such as oil and gas), greases, and similar materials.
+   Type C fires involve energized electrical equipment.