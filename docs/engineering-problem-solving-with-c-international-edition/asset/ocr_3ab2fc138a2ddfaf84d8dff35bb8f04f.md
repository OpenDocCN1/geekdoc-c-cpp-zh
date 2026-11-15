![](bbox=[0.32, 0.08, 0.8, 0.35])

Figure 5.7 Three-dimensional array.

Most engineering problems that need arrays can be solved using one-dimensional or two-dimensional arrays. However, there are occasionally problems that are good candidates for using higher dimensional arrays. These problems typically involve data that are specified by several parameters; in addition, the parameters are either integers that are sequential or parameters that can easily be converted into sequential parameters. For example, suppose that a set of data representing temperature measurements is taken from the floor of a large chemical reaction chamber. Furthermore, this set of temperatures is taken at specified intervals of time during a chemical reaction. In this case, we might choose to use a three-dimensional array, using the first subscript to indicate a specific time and the other two subscripts to indicate the location within the floor. The subscripts would need to begin with zero to match the requirements of C subscripts. The subscripts [3] [2] [5] would then specify the value taken at the fourth time value, and at position [2] [5] in the grid of temperatures.

Arrays with over three subscripts are seldom used, because it is difficult to visualize them. However, a simple way to visualize arrays with over three subscripts can be developed. First, imagine that a three-dimensional array is a building. The building has floors, and it also has a rectangular grid of rooms on each floor. Assume each room can contain a single value. The three-dimensional array representing the building uses three subscripts to specify a room; the first subscript is the floor number and the other two subscripts specify the row and column number of the room on the specified floor.

Four-dimensional array

A four-dimensional array is a row of buildings, as shown in Figure 5.8. The first subscript specifies the building, and the remaining three subscripts specify the room in the building.

![](bbox=[0.22, 0.81, 0.9, 0.89])

Figure 5.8 Four-dimensional array.