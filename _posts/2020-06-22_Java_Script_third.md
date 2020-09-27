---
title: "JavaScript - part3"
date: 2020-06-22 23:00:00
categories: programming
---
### DOM Event Listening

```js
//button
var button = d3.select("#click-me")
button.on("click",function(){
    console.log(d3.event.target);
});
```
```js
//textbox input field
var inputField = d3.select("#input-field")
inputField.on("change", function(){
    var newText = d3.event.target.value;
    console.log(newText);
};
```
```js
//textbox input 
var text = d3.select("#text");
function handleChange(event){
   var inputText=d3.event.target.value;
   console(inputText);
}
text.on("change",handleChange);
```
```js
//this
d3.selectAll('button').on('click',function(){
     console.log(this);
});
d3.selectAll('li').on('click',function(){
    var listItem = d3.select(this);
    listItem.style("color","blue");
    console.log(listItem.text());
});
```
```js
//Form
var button = d3.select("button");
var form = d3.select("#form");
button.on("click",runEnter);
form.on("submit",runEnter);
function runEnter(){
   d3.event.preventDefault();
   var inputElement = d3.select("#example-form-input");
   var inputValue = inputElement.property("value");
   d3.select("h1>span").text(inputValue);
}
```
