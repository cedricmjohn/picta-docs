---
id: chart
title: Chart
sidebar: sidebar
permalink: chart.html
folder: components
summary: Charts structure how the graph is rendered
---

### Introduction

Charts are created from multiple Components, and are highly customizable. The best way to get acquainted with charts is to create different types of plots.

### Creating a Chart

The following is the constructor for the chart. Now in practice not all of these items need to be individually specified. The example will make this clearer.

 * ```series```: A list of series we wish to plot.
 * ```layout```: This specifies how the chart will be laid out.
 * ```config```: This configures the chart.
 * ```animated```: This specifies whether the chart is animated.
 * ```transition_duration```: If the chart is animated, this specifies the duration between the frames.



### The Chart in Action

As the following example makes  clear, we do not need to specify every single Component that constructs a Chart fully. We can sculpt the Chart specifying options where we need to.

An example can be found here: [Your First Chart](/first_chart.html)