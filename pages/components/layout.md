---
id: layout
title: Chart Layout
sidebar: sidebar
permalink: layout.html
folder: components
summary: Chart Layouts specify in detail how the plot will be rendered
---

### Introduction

Chart Layouts map to a single chart. They determine how the chart itself is displayed on screen. Usually Chart Layouts do not need to be directly specified, and we can use methods inside the Chart component to manipulate the underlying layout options. However, in certain cases more control may be required.

### Specifying a Chart Layout

The following is the constructor for the chart. Now in practice not all of these items need to be individually specified; a better approach is to use the Chart component to craft a chart, then dive down to a lower component as and when needed.

*  ```title```      : Sets the chart title.
* ``` axes```       : Sets the chart title.
* ``` showlegend``` : Specifies whether to show the legend.
* ``` autosize```   : This is the component that configures the legend for the chart..
* ``` legend```     : This is the component that configures the legend for the chart..
* ``` height```     : This sets the height for the chart.
* ``` width```      : This sets the width for the chart.
* ``` mapoption```  : this is used for Map charts only and configures the Map chart.