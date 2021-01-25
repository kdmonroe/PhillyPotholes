---
title: "Altair - Philadelphia Potholes by Neighborhood"
date: 2019-05-13
show_date: false
read_time: false
published: true
tags: [dataviz, altair, vega-lite]
excerpt: "City Potholes by Neighborhood"
altair-loader:
  altair-chart: "charts/measlesAltair.json"
toc: true
toc_sticky: true
---

## Altair Example

Below is a chart of the city potholes in the last 107 days. Note: this visualization package is limiting to 5000 observations.

<div id="altair-chart"></div>

The code below is HTML for the desired template to match with the above chart, which had a slider for the number of selection of days. This works locally but not sure how to embed within GitHub Pages.

```python
# HTML code for template 2 -
# template for embedding slider to select for number of days
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
        Below, we show the number of potholes throughout Philadelphia
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
```
