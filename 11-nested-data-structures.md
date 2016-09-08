#### [⇐ Previous](./10-objects-and-arrays.md) | [Table of Contents](./readme.md) | [Next ⇒](./12-functions-and-scope.md)

# Nested Data Structures

### Objectives:

By the end of this chapter - you should be able to

- Create nested data structures using objects and arrays
- Access and iterate over data in a nested data structure
- Add and remove data inside of a complex data structure

### What is a data structure? A nested one?

So what do we mean by data structure? From Wikipedia - "In computer science, a data structure is a particular way of organizing data in a computer so that it can be used efficiently." So far we have seen `Objects` and `Arrays` as our way of organizing data (there are many many more we will examine over this class), but in JavaScript, these two can get us very far.

So what is a nested data structure? It just means one data structure inside of another! Let's see some an example:

```javascript

var instructorData = {
    name: "Elie",
    additionalData: {
        instructor: true,
        favoriteHobbies: ["Playing Cello", "Tennis", "Coding"],
        moreDetails: {
            favoriteBasketballTeam: "New York Knicks",
            numberOfSiblings: 3,
            isYoungest: true,
            hometown: {
                city: "West Orange",
                state: "NJ",
            },
            citiesLivedIn: ["Seattle", "Providence", "New York"]
        }
    }
}

instructorData.name // "Elie"
instructorData.additionalData.instructor // true
instructorData.additionalData.favoriteHobbies[2] // "Coding"
instructorData.additionalData.moreDetails.favoriteBasketballTeam // "New York Knicks"
instructorData.additionalData.moreDetails.homeTown.state // "NJ"
instructorData.additionalData.moreDetails.citiesLivedIn[1] // "Providence"
```

So you may be thinking - am I really going to be working with data like this? Seriously? The answer is a strong **YES**! Very commonly, when you receive large amounts of data from third parties, you will be given it in a format that includes nested objects/arrays. It is imperative you understand how to access data in these nested data structures. Copy and paste the previous example in chrome console or make up your own to practice!

### 2D Arrays

When working with two dimensional arrays, if you want to print out all of the values, you are going to need a loop inside of a loop! Let's examine that a bit further.

```javascript
var nestedArr = [[1,2], [3,4]]
for(var i=0; i<nestedArr.length; i++){
    console.log(nestedArr[i])
}

// this will log out...
// [1,2]
// [3,4]
```

But what if we want to print out each individual value? We will need another loop inside of the first loop! We traditionally initialize the inner counter as `j` (what comes after `i`) and we will loop as long as `j` is less than the length of **each** inner array.

```javascript
var nestedArr = [[1,2], [3,4]]
for(var i=0; i<nestedArr.length; i++){
    for(var j=0; j<nestedArr[i].length; j++){
        // notice that we are going inside the outer array
        // and now inside of the inner array
        console.log(nestedArr[i][j])
    }
}

// this will log out...
// 1
// 2
// 3
// 4
```

Here is an another example - take a quick look and try to replicate it without looking at the code!

```javascript
var nestedArr = [[1,2,3], [4,5,6], [7,8,9]]
for(var i=0; i< nestedArr.length; i++){
    for(var j=0; j<nestedArr[i].length; j++){
        console.log(nestedArr[i][j])
    }
}
```

So when are two-dimensional arrays used? Quite often! When building games you think of a game board like a nested array. You can use a nested array for a tic-tac-toe board, a minesweeper board, maybe for a couple hands of poker! 

### Writing functions to produce values in a nested data structure

Let's use our same example from above:

```javascript
var instructorData = {
    name: "Elie",
    additionalData: {
        instructor: true,
        favoriteHobbies: ["Playing Cello", "Tennis", "Coding"],
        moreDetails: {
            favoriteBasketballTeam: "New York Knicks",
            numberOfSiblings: 3,
            isYoungest: true,
            hometown: {
                city: "West Orange",
                state: "NJ",
            },
            citiesLivedIn: ["Seattle", "Providence", "New York"]
        }
    }
}

// write a function that console.log's all the cities lived in
function displayCities(){
    var cityArray = instructorData.additionalData.moreDetails.citiesLivedIn
    for(var i=0; i< cityArray.length; i++){
        console.log(cityArray[i])
    }
}

// write a function that console.log's all the values of the hometown object
function displayHometownData(){
    var hometownObject = instructorData.additionalData.moreDetails.hometown
    for(var key in hometownObject){
        console.log(hometownObject[key])
    }
}
// write a function that adds a key and value to the moreDetails object and returns the object
function addDetail(key,value){
    var detailsObject = instructorData.additionalData.moreDetails
    detailsObject[key] = value;
    return detailsObject
}

// write a function that removes a key in the moreDetails object and returns the object
function removeDetail(key){
    var detailsObject = instructorData.additionalData.moreDetails;
    var valueToBeRemoved = detailsObject[key];
    delete detailsObject[key];
    return valueToBeRemoved;
}

```

### Exercise

Complete the [Nested Data Structures Exercise](https://github.com/rithmschool/prework_exercises/tree/master/nested_objects_exercise)

### Additional Resources

An excellent post on accessing nested resources - [http://stackoverflow.com/questions/11922383/access-process-nested-objects-arrays-or-json](http://stackoverflow.com/questions/11922383/access-process-nested-objects-arrays-or-json)

#### [⇐ Previous](./10-objects-and-arrays.md) | [Table of Contents](./readme.md) | [Next ⇒](./12-functions-and-scope.md)