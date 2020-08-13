---
id: config
title: Config
sidebar: sidebar
permalink: config.html
folder: components
summary: Config specifies interactivity of a chart
---

### Introduction

Sometimes we may want to turn some of the interactive features of a plot off. We can do this by setting the Config. The easiest way to do this is to operate directly on the ```Chart``` component.

The following example demonstrates how to use the ```setConfig``` method:

```scala
val chart = Chart() addSeries series setTitle "My Chart" setConfig(responsive=false, scrollZoom=false)
```