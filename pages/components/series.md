---
id: series
title: Series
sidebar: sidebar
permalink: series.html
folder: components
summary: Series components wrap data and specify how they should be transformed
---

### Introduction

The ```Series``` component represents the data that we wish to plot. The ```Series``` component comes in three flavours:

* ```XY```: This represents 2D data.
* ```XYZ```: This represents 3D data.
* ```Map```: This represents data for a Map plot.

### Composing a Series

Suppose we wanted to create a 2D series with the following properties:

* 2D data from lists ```x``` and ```y```
* Represent the series as a Scatter chart
* Style the plot with Markers (as opposed to Lines)

The code to do this will look as follows:

```scala
val series = XY(x, y)
            .asType(SCATTER)
            .drawMarkers 
```