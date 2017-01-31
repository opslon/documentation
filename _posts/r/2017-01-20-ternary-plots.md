---
title: Ternary Plots in R | Examples | Plotly
name: Ternary Plots
permalink: r/ternary-plots/
description: How to create ternary plots in R with Plotly.
layout: base
thumbnail: thumbnail/ternary.jpg
language: r
page_type: example_index
has_thumbnail: true
display_as: scientific
order: 13
output:
  html_document:
    keep_md: true
---


### New to Plotly?

Plotly's R library is free and open source!<br>
[Get started](https://plot.ly/r/getting-started/) by downloading the client and [reading the primer](https://plot.ly/r/getting-started/).<br>
You can set up Plotly to work in [online](https://plot.ly/r/getting-started/#hosting-graphs-in-your-online-plotly-account) or [offline](https://plot.ly/r/offline/) mode.<br>
We also have a quick-reference [cheatsheet](https://images.plot.ly/plotly-documentation/images/r_cheat_sheet.pdf) (new!) to help you get started!

### Version Check

Version 4 of Plotly's R package is now [available](https://plot.ly/r/getting-started/#installation)!<br>
Check out [this post](http://moderndata.plot.ly/upgrading-to-plotly-4-0-and-above/) for more information on breaking changes and new features available in this version.

```r
library(plotly)
packageVersion('plotly')
```

```
## [1] '4.5.6.9000'
```

### Set Layout


```r
library(plotly)

# acquire data
ds <- jsonlite::fromJSON(
  "https://gist.githubusercontent.com/davenquinn/988167471993bc2ece29/raw/f38d9cb3dd86e315e237fde5d65e185c39c931c2/data.json"
)
df <- dplyr::bind_rows(ds, .id = "id")

# reusable function for creating annotation object
label <- function(txt) {
  list(
    text = txt, 
    x = 0.1, y = 1,
    ax = 0, ay = 0,
    xref = "paper", yref = "paper", 
    align = "center",
    font = list(family = "serif", size = 15, color = "white"),
    bgcolor = "#b3b3b3", bordercolor = "black", borderwidth = 2
  )
}

# reusable function for axis formatting
axis <- function(txt) {
  list(
    title = txt, tickformat = ".0%", tickfont = list(size = 10)
  )
}

ternaryAxes <- list(
  aaxis = axis("Clay"), 
  baxis = axis("Sand"), 
  caxis = axis("Silt")
)
```

### Add Markers


```r
library(plotly)
library(jsonlite)
 
p <- plot_ly(
  df, a = ~clay, b = ~sand, c = ~silt, color = I("black"), type = "scatterternary"
) %>%
  layout(
    annotations = label("Ternary Markers"), ternary = ternaryAxes
  )

# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = plotly_POST(p, filename="ternary/markers")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/4264.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>

### Add Lines


```r
library(plotly)
library(jsonlite)
 
p <- plot_ly(
  df, a = ~clay, b = ~sand, c = ~silt, color = I("black"), type = "scatterternary", 
  split = ~id, mode = "lines"
) %>%
  layout(
    annotations = label("Ternary Lines"), ternary = ternaryAxes
  )

# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = plotly_POST(p, filename="ternary/lines")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/4266.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>

### Add Contour


```r
library(plotly)
library(jsonlite)
 
p <- plot_ly(
  df, a = ~clay, b = ~sand, c = ~silt, color = ~id, type = "scatterternary",
  fill = "toself", mode = "lines"
) %>%
  layout(
    annotations = label("Ternary Contour"), ternary = ternaryAxes
  )


# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = plotly_POST(p, filename="ternary/contour")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/4268.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>

#Reference

See [https://plot.ly/r/reference/#scatterternary](https://plot.ly/r/reference#scatterternary) for more information and options!