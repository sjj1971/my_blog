---
title: "Plotly - part1"
date: 2020-06-24 00:30:00
categories: programming
---
### Plotly
```js
//Drawing plot using plotly
var trace1 = { x: [...], y: [...], type: "bar" }; // chart types : "bar", "line"
var data = [trace1];
var layout = { title: "Bar chart", xaxis: {title: "X Data"}, yaxis: {title: "Y Data"} };
Plotly.newPlot("plot",data,layout); // "plot" is the tag in html
```
```js
//Drawing pie chart using plotly
var trace1 = { labels: [...], values: [...], type:'pie'};
var data = [trace1]
var layout = { title: "Pie chart"};
Plotly.newPlot("plot", data, layout);
```
```js
//multi trace
var trace1 = {
  x: data.map(row => row.pair),
  y: data.map(row => row.greekSearchResults),
  text: data.map(row => row.greekName),
  name: "Greek",
  type: "bar"
};
var trace2 = {
  x: data.map(row => row.pair),
  y: data.map(row => row.romanSearchResults),
  text: data.map(row => row.romanName),
  name: "Roman",
  type: "bar"
};
var data = [trace1, trace2];
var layout = {
  title: "Greek vs Roman gods search results",
  barmode: "group"
};
Plotly.newPlot("plot", data, layout);
```
```js
//Box plot
var trace1 = { y : [.....], type: "box" };
var trace2 = { y : [.....], type: "box" };
var data = [trace1, trace2]
var layout = {title: "Basic Box Plot"}
Plotly.newPlot("plot", data, layout)
```
```js
//Grouped Box plot
var x = ['day 1', 'day 1', 'day 1', 'day 1', 'day 1', 'day 1', 'day 2', 'day 2', 'day 2', 'day 2', 'day 2', 'day 2']
var trace1={y:[0.2, 0.2, 0.6, 1.0, 0.5, 0.4, 0.2, 0.7, 0.9, 0.1, 0.5, 0.3],x:x,name:'kale',marker:{color:'#3D9970'},type:'box'};
var trace2={y:[0.6, 0.7, 0.3, 0.6, 0.0, 0.5, 0.7, 0.9, 0.5, 0.8, 0.7, 0.2],x:x,name:'radishes',marker:{color:'#FF4136'},type:'box'};
var data = [trace1, trace2];
Plotly.newPlot("plot, data)
```
