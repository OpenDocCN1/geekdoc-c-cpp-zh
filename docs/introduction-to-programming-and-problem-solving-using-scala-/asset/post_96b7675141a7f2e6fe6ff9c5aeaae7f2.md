
![](img/06d4e84f27a8884ea40ba6182ec7c778_403_0.png)

**FIGURE 12.13:** The window that is produced by running ImageEffects.scala with four sample images. The top-left and bottom-right images were set to the ColorAdjust effect, the top-right used SepiaTone, and the bottom-left used Glow.

## 12.8 Charts

A common task done on computers when you have data sets is to use charts to plot the data. For this reason, ScalaFX includes a scalafx.scene.chart package with a number of different chart types as well as other types that are required to build these charts. There are eight different types that are part of the library. These are as follows:

- AreaChart - Fills in an area from zero up to a line for one or more sequences of numeric x-y data.
- BarChart - Displays data as bars for different text categories.
- BubbleChart - Draws bubbles of various sizes at numeric x-y coordinates.
- LineChart - Draws a line for a sequence of numeric x-y data.
- PieChart - Draws a pie chart for a sequence of labeled numeric data.
- ScatterChart - Draws a scatter chart for a sequence of x-y data.
- StackedArea - Draws area charts stacked on top of one another for multiple series of x-y data.
- StackedBarChart - Draws bars stacked on top of one another for different categories.

With the exception of PieChart, all the charts inherit from XYChart, which is not listed here because it is abstract. All of the subtypes of XYChart require two axes as well as the data to be plotted. Scala provides three different types of Axis including CategoryAxis for text categories and NumberAxis for numeric values.
To help the use of these charts in a program, the following creates three different charts, a PieChart, a BarChart, and a ScatterChart, based on data about our solar system.

Listing 12.13: Charts.scala

```
import scalafx.Includes.
import scalafx.application.JFXApp
import scalafx.scene.Scene
import scalafx.scene.chart.
import scalafx.scene.control.
import scalafx.scene.layout.
import scalafx.collections.ObservableBuffer
import scalafx.geometry.Pos

val app = new JFXApp {
  stage = new JFXApp.PrimaryStage {
    title = "Charts"
    scene = new Scene(1000, 800) {
      class PlanetData(name:String, mass:Double, radius:Double)
      val planets = List(
        PlanetData("Mercury", 0.0553, 0.387),
        PlanetData("Venus", 0.815, 0.723),
        PlanetData("Earth", 1.0, 1.0),
        PlanetData("Mars", 0.107, 1.524),
        PlanetData("Jupiter", 31.83, 5.203)
      )
    }
  }
}
```

## Graphics and ScalaFX

PlanetData("Saturn", 95.159, 9.537)
PlanetData("Uranus", 14.536, 19.191)
PlanetData("Neptune", 17.147, 30.069)

```
val pieChart = PieChart(ObservableBuffer(planets.map(p =>
    PieChart.Data(p.name, p.mass))))

val barSeries = XYChart.Series("Planetary Mass",
ObservableBuffer(planets.map(p => XYChart.Data(p.name,
    p.number))))

val barChart = BarChart(CategoryAxis("Mass [Earth Mass]"),
ObservableBuffer(barSeries))

val scatterSeries = XYChart.Series("Mass vs. Orbital Distance",
ObservableBuffer(planets.map(p => XYChart.Data(p.a,
    p.mass))))

val scatterChart = ScatterChart(NumberAxis("Semimajor Axis [AU]"),
NumberAxis("Mass [Earth Mass]"), ObservableBuffer(scatterSeries))

val tilePane = new TilePane
tilePane.children = List(pieChart, barChart, scatterChart)
tilePane.alignment = Pos.TopCenter

root = tilePane
```

The result of running this code can be seen in figure 12.14. As usual, the code begins with a number of imports, this time includes scalafx.scene.chart. That is followed by the general setup of the app, the stage and the scene. Lines 14-22 define a case class and a list of instances that it provide the data to be used for plots. This data has the planets in our Solar System with their masses in units of Earth mass and the semimajor axis (average distance from the Sun) in AU.¹

Line 24 creates a PieChart to show how much of the solar system, outside of the Sun, is in. This is done by passing PieChart ObservableBuffer filled with PieChart data. All the charts in ScalaFX will update if the values are changed. This can be used to see some effect in some applications. There is also a property of the charts called animated that will cause such changes to be animated if it is set to true. In this case.

The result of running this code can be seen in figure 12.14. As usual, the code begins with a number of imports, this time includes scalafx.scene.chart. That is followed by the general setup of the app, the stage and the scene. Lines 14-22 define a case class and a list of instances that it provide the data to be used for plots. This data has the planets in our Solar System with their masses in units of Earth mass and the semimajor axis (average distance from the Sun) in AU.¹

Line 24 creates a PieChart to show how much of the solar system, outside of the Sun, is in. This is done by passing PieChart ObservableBuffer filled with PieChart data. All the charts in ScalaFX will update if the values are changed. This can be used to see some effect in some applications. There is also a property of the charts called animated that will cause such changes to be animated if it is set to true. In this case.

**FIGURE 12.13:** The window that is produced by running ImageEffects.scala with four sample images. The top-left and bottom-right images were set to the ColorAdjust effect, the top-right used SepiaTone, and the bottom-left used Glow.

**FIGURE 12.14:** Charts.scala.
