---
id: contributing_docs
title: Contributing To The Library
sidebar: sidebar
permalink: contributing_library.html
folder: pages
summary: This section exlains how to contribute to the library codebase.
---

## Testing Requirements

If you have NPM installed, you can simply navigate to `/src/test/resources/javascript` and run the following command in your terminal:

```
npm install
```

This should install install all the necessary dependencies using `NPM` to get the unit-testing framework working correctly.

Run the following command using the `sbt` shell to see if your code compiles and can run the test suite:

```
+ test
```

You should see the unit tests run and give you an output indicating how many test cases passed or failed. You are now ready to
add more functionality to the codebase.

## Adding functionality

In Picta each component is represented by a case class.

Each component is a set of (key, value) pairs that can be serialized to a JSON object. A plot combines several components together
and produces a combined JSON object that is equivalent to a Plotly.js chart schema.

To add functionality, one needs to make sure that the combined JSON object is a valid Plotly.js schema. This means that valid (key, value)
pairs must be added to the correct component.

To see a full list of valid (key, value) pairs, consult the Plotly.js [figure reference](https://plotly.com/javascript/reference/).

## Example

For a concrete example, consider the `ChartLayout` component:

```scala
final case class ChartLayout
  (title: Opt[String] = Blank, axes: Opt[List[Axis]] = Empty, legend: Opt[Legend] = Blank,
  auto_size: Opt[Boolean] = Blank, margin: Opt[Margin] = Blank,map_options: Opt[MapOption] = Blank,
  multi_chart: Opt[MultiChart] = Blank,hover_distance: Opt[Int] = Blank, show_legend: Boolean = true,
  hover_mode: HoverMode = CLOSEST, height: Int = 550, width: Int = 600,
 private[picta] val XYZ: Boolean = false)
extends Component {

  def setTitle(new_title: String) = this.copy(title = new_title)

  def setAxes(new_axes: List[Axis]) = axes.option match {
    /* add to the end of existing list. This ensures things that when we have two of the same keys,
    the ones at the right are preserved. This is because below we foldleft when merging the axes */
    case Some(lst) => this.copy(axes = lst ::: new_axes)
    case None => this.copy(axes = new_axes)
  }

  def setAxes(new_axis: Axis*) = axes.option match {
    /* add to the end of existing list. This ensures things that when we have two of the same keys,
    the ones at the right are preserved. This is because below we foldleft when merging the axes */
    case Some(lst) => this.copy(axes = lst ::: new_axis.toList)
    case None => this.copy(axes = new_axis.toList)
  }

  def setLegend(new_legend: Legend) = this.copy(legend = new_legend, show_legend = true)

  def setLegend(x: Opt[Double] = Blank, y: Opt[Double] = Blank, orientation: Orientation = VERTICAL,
                xanchor: Opt[Anchor] = Blank, yanchor: Opt[Anchor] = Blank) = {

    val new_legend = Legend(x = x, y = y, orientation = orientation, xanchor = xanchor, yanchor = yanchor)
    this.copy(legend = new_legend)
  }

  def setAutosize(new_autosize: Boolean) = this.copy(auto_size = new_autosize)

  def setMargin(new_margin: Margin) = this.copy(margin = new_margin)

  def setMapOption(new_geo: MapOption) = this.copy(map_options = new_geo)

  def setMultiChart(new_minigrid: MultiChart) = this.copy(multi_chart = new_minigrid)

  def showLegend(new_showlegend: Boolean) = this.copy(show_legend = new_showlegend)

  def setHoverMode(new_hovermode: HoverMode) = this.copy(hover_mode = new_hovermode)

  def setHeight(new_height: Int) = this.copy(height = new_height)

  def setWidth(new_width: Int) = this.copy(width = new_width)

  def setDimensions(new_height: Int, new_width: Int) = this.copy(height = new_height, width = new_width)

  private[picta] def setXYZ(XYZ: Boolean) = this.copy(XYZ = XYZ)

  private[picta] def serialize: Value = {
    val dim = Obj("height" -> height, "width" -> width, "hovermode" -> hover_mode.toString.toLowerCase)

    val title_ = title.option match {
      case Some(x) => Obj("title" -> Obj("text" -> x))
      case None => jsonMonoid.empty
    }

    val showlegend_ = Obj("showlegend" -> show_legend)

    val autosize_ = auto_size.option match {
      case Some(x) => Obj("autosize" -> x)
      case None => jsonMonoid.empty
    }

    val geo_ = map_options.option match {
      case Some(x) => Obj("geo" -> x.serialize)
      case None => jsonMonoid.empty
    }

    val margin_ = margin.option match {
      case Some(x) => Obj("margin" -> x.serialize)
      case None => jsonMonoid.empty
    }

    val minigrid_ = multi_chart.option match {
      case Some(x) => Obj("grid" -> x.serialize)
      case None => jsonMonoid.empty
    }

    val legend_ = legend.option match {
      case Some(x) => Obj("legend" -> x.serialize)
      case _ => jsonMonoid.empty
    }

    val hoverdistance_ = hover_distance.option match {
      case Some(x) => Obj("hoverdistance" -> x)
      case _ => jsonMonoid.empty
    }

    val combined = List(dim, title_, showlegend_, autosize_, geo_, margin_, minigrid_, legend_, hoverdistance_)
      .foldLeft(jsonMonoid.empty)((a, x) => a |+| x)

    axes.option match {
      case Some(lst) =>
        if (XYZ == true) {
          val combined_axes = lst.foldLeft(jsonMonoid.empty)((a, x) => a |+| x.serialize)
          val scene = Obj("scene" -> combined_axes)
          List(scene).foldLeft(combined)((a, x) => a |+| x)
        }
        /* if we have a XY chart, we can filter out the zaxis as they will never be used */
        else lst.filter(axis => axis.orientation != "zaxis").foldLeft(combined)((a, x) => a |+| x.serialize)
      case _ => combined
    }
  }
}
```

As can be seen from the `ChartLayout` component above, the constructor takes in a number of parameters. The name of the parameter is the corresponding
key, while it's value is the corresponding value in the (key, value) pair that is inserted into a JSON object. Inside the component there is a `serialize`
method that combines all of these (key, value) pairs into a single JSON object.

To extend this component, simply add an argument to the constructor, and ensure it is added to the JSON object when the `serialize` method is called.

## Adding A Unit Test

Once you have added new functionality, add a new test to check that it still gives a valid Plotly.js JSON schema. To do this first navigate to
`/src/test/scala/test`. Add a new test case using the [ScalaTest](https://www.scalatest.org) library, and call the `validateJson` function within your test
body, inside an `assert` statement to check whether the test passes or fails. All unit tests should pass before the additional code will be accepted.
