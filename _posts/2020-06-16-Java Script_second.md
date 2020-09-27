---
title: "JavaScript - part2"
date: 2020-06-16 11:00:00
categories: programming
---
### DOM

```js
//d3.select("class")
d3.select(".text1").text("Time to change the text")
d3.select(".text1").html()
```
```js
//select all
d3.selectAll('li').style('color','blue');
```js
// select child class and selecting attribute
var myLInkAnchor = d3.select(".my-link > a")
var myLinkAnchorAttribute = myLinkAnchor.attr("href")
// setting attribute
myLinkAnchor.attr("href","https://python.org");
```
```js
d3.select("ul").selectAll("li").each(function(d,i){
    console.log("element", this);
    console.log("data", d);
    console.log("index", i);
});
```js
//chaining
d3.select(".my-link>a").attr("href", "https://nytimes.org").text("Now this is a link to the NYT");
```
```js
//create a new element
var li1 = d3.select('ul').append('li');
li1.text('A new Item has been added!);
var li2 = d3.select('ul').append('li').text('Another new Item');
```
```js
//Adding table
var tbody = d3.select('tbody');
data.forEach(function(weatherReport){
    var row = tbody.append('tr');
    Object.entries(wetherReport).forEach(function([key, value]){
       var cell = row.append('td');
       cell.text(value);
    });
});
```
