---
title: "Picta"
keywords: homepage
tags: [getting_started]
sidebar: sidebar
permalink: index.html
summary: Picta is a graphing library for Scala. It is designed to be easy to use and allows charts to be composed from simpler components.
---

## What is Picta?

Picta is a graphing library for the Scala programming language built by the Carbonate Research Lab at Imperial College London.

The goal of Picta is to be an easy to use, composable graphics library.

If you would like to see an overview of the types of charts that can be created by Picta, navigate, click on the `Example Gallery` link on the left sidebar.

We felt that such a library was missing from the Scala, and indeed the JVM ecosystem.

Picta provides the following benefits over existing libraries:

- **Expressive API**: Picta reduces boilerplate by creating a DSL that users can leverage to write expressive plot compositions in a minimal amount of code.

- **Interactive Plots**: Charts are interactive and can be used to actively explore the data sets.

- **Extensive Functionality**: Picta can create many different types of plots that are useful for exploratory visual analysis.

- **Jupyter Integration**: Picta fully supports the Almond kernel, and so can become an integral part of the scientific workflow.

Often libraries are limited in functionality, require large amounts of boilerplate, or are just fundamentally **not_fun_to_use**.

## How does it work?

Under the hood Picta uses [Plotly.js](https://plotly.com/javascript/) for rendering. Every Picta plot is therefore valid HTML that can simply be displayed in your browser. No need for clunky JVM GUI dependencies that make you feel like you are programming back in the 90s. Picta simply uses the browser you love to display the charts you need.

In addition to rendering standalone HTML pages, Picta also work's with the Almond Jupyter Kernel. This allows the library to be used in way traditionally associated with Python's matplotlib library.

Support for further Scala Notebook kernels, such as [Zeppelin](https://zeppelin.apache.org) will be added in the future.

## How is it different to other libraries?

If you use Picta for charting it will **_feel_** different from other libraries available on the JVM, and not because it is channeling some kind of cosmic energy direct in to your brain.

The real reason is, unlike other libaries, Picta attempts to define a simple way to create charts, inspired in part by Leland Wilkinson's **Grammar of Graphics** approach.

## Installing the library

Follow these instructions to install Picta on your machine.

## Installation

### sbt

Add the following lines to your sbt project:

```scala
libraryDependencies  += "org.carbonateresearch" %% "picta" % "0.1.1"
resolvers += "jitpack" at "https://jitpack.io"
```

You should now be good to go using the library on your JVM projects!

### Almond Jupyter kernel

Add the following to the start of your notebook:

```scala
interp.repositories() ++= Seq(coursierapi.MavenRepository.of(
  "https://jitpack.io"
))

import $ivy. `org.carbonateresearch::picta:0.1.1`
```

<!-- {% include links.html %} -->
