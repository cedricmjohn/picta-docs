---
id: marker_styles
title: Marker Styles
sidebar: sidebar
permalink: marker_styles.html
folder: styling
summary: This section will outline how markers may be styled, and what the different options for marker shapes are
---

### Intro

Markers can be extensively styled with many different shapes available. In order to style a marker, we can do the following:

```scala
// we import the marker option which lets us specify the marker
import org.carbonateresearch.picta.options.Marker
import org.carbonateresearch.picta.SymbolShape._
```

```scala
// lets give the second series a red marker. Again we can 'compose' a marker using smaller components
val marker = Marker() setSymbol SQUARE_OPEN setColor "red"

val series = XY(x, y) asType SCATTER setName "Scatter" drawStyle MARKERS setMarker marker

// we not put brackets in the 'addSeries' function to ensure that addSeries picks up the right series'
val chart = Chart() addSeries(series) setTitle("Multiple series on one chart")

chart.plotInline
```

The crucial step is the ```setSymbol``` method which sets the markers to a red open square symbol.

This will produce the following example:

![marker_style](images/styling/marker_style.png)

A full list of symbol shapes can be found in the API docs here:

[Marker Styles](https://acse-fk4517.github.io/picta-api/org/carbonateresearch/picta/SymbolShape$.html)