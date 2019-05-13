---
title: "1 Chart, 3 Libraries"
date: 2019-05-13
published: true
tags: [dataviz, altair, vega-lite, observable, holoviews]
excerpt: "Embedding interactive charts on static pages using Jekyll."
altair-loader:
  altair-chart: "charts/measlesAltair.json"
observable-loader:
  url: https://api.observablehq.com/@nickhand/embedding-altair-plots-in-observable.js
  names:
    vega-chart: "heatmap"
hv-loader:
  holoviews-chart: "charts/measlesHoloviews.html"
toc: true
toc_sticky: true
---

This post will show examples of embedding interactive charts produced using [Altair](https://altair-viz.github.io) [Vega-Lite](https://vega.github.io/vega-lite/) via [Observable](https://observablehq.com/), and
[Holoviews](http://holoviews.org/index.html).

## Altair Example

Below is a chart of the incidence of measles since 1928 for the 50 US states.

<div id="altair-chart"></div>

This was produced using Altair and embedded in this static web page. Note that you can also display Python code on this page:

```python
import altair as alt
alt.renderers.enable('notebook')
```

<!DOCTYPE html>
<html lang="en">
  <!-- Start of the Header -->

  <head>
    <title>Flasked Altair</title>
    <meta charset="utf-8" />

    <!-- This is boiler plate styling for Altair -->
    <style>
      .vega-actions a {
        margin-right: 12px;
        color: #757575;
        font-weight: normal;
        font-size: 13px;
      }

      .error {
        color: red;
      }
    </style>

    <!-- Load a better style file -->
    <link rel="stylesheet" href="https://codepen.io/chriddyp/pen/bWLwgP.css" />

    <!-- Load Javascript for Vega-Related Libraries -->
    <script
      type="text/javascript"
      src="https://cdn.jsdelivr.net/npm//vega"
    ></script>
    <script
      type="text/javascript"
      src="https://cdn.jsdelivr.net/npm//vega-lite"
    ></script>
    <script
      type="text/javascript"
      src="https://cdn.jsdelivr.net/npm//vega-embed"
    ></script>
  </head>
  <!-- End of the Header -->

  <body>
    <div class="container">
      <!-- Add a header -->
      <h1>Potholes in Philadelphia</h1>

      <!-- Add a paragraph of text -->
      <p>
        Below, we show the number of fatal/nonfatal shootings in Philadelphia
        grouped by neighborhood.
      </p>

      <!-- Add a range slider -->
      <div class="slider">
        Select the number of days to query:
        <input
          type="range"
          min="30"
          max="365"
          step="1"
          value="365"
          onchange="embedChart(`/chart?days=${this.value}`, 'chart')"
        />
      </div>

      <!-- the div element to embed the chart -->
      <div id="chart"></div>
    </div>

    <!-- Render Charts: this has to be at the end!-->
    <script type="text/javascript">
      function embedChart(url, div) {
        // call vegaEmbed for the JSON spec
        vegaEmbed(`#${div}`, url)
          .then(function(result) {})
          .catch(console.error);
      }

      // run the function that embeds the chart
      embedChart("/chart", "chart");
    </script>
  </body>
</html>
