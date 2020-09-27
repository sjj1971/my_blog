---
title: "JavaScript - part1"
date: 2020-06-03 18:00:00
categories: programming
---

## Reference
```html
### You Don't Know JS book series :
<a href="https://github.com/getify/You-Dont-Know-JS">https://github.com/getify/You-Dont-Know-JS</a>

link: https://github.com/getify/You-Dont-Know-JS

### JavaScript Tutorial: https://watchandcode.com/p/practical-javascript
### INteractive JaveScript Sheet: https://htmlcheatsheet.com/js/
### Scrimba Intro to JvaScript: https://scrimba.com/g/gintrotojavascript
### Plotly Getting Started with plotly : https://plotly.com/javascript/getting-started/
```
```js
//changing datatype
parseInt(string);
```
```js
//forEach
var students = ["Johnny", "Alice", "Mike"]
students.forEach(printName); // it is same to call printName[i] for i in students list 
students.forEach(function(item)){ // it is to use anonymous function without prior definition.
   console.log(item)
}
```
```js
//Anonymous function simplification
(item) => { return item;}
(item) => item;
var mapSimpleArray = theStageOfJS.map(
    (item) => item;
);

var mapArrayWithIndex = theStageOfJS.map(
(item, index)=> `Stage ${index}:${item}`
);
```

```js
//Dictionary is Object in JS
Object.keys(movie);
Object.values(movie);
Object.entries(movie);
movie.rating = 6.5;
if (rating in movie){
    console.log("movie has rating")
};
```
```js
//using map is like enumerate in pythonerrow but using with return
var mapSimpleArray = theStageOfJS.map(function(item, index) {
    return `Stage $ {index+1} : $ {item}`
```
```js
//handling array of objects
var users = [{}, {}, {}]
users.forEach(user =>{
   console.log(user);
   Object.entries(user).forEach([key, value] => console.log('key:${key} and value ${value}'));
})
```
```js
//filter
function selectYounger(person){
    return person.age <30;
}
var youngSimpsons = simpsons.filter(selectYounger);
```
```js
//filter simple version
var youngSimpsons = simpsons.filter(person => person.age<30);
```

