---
layout: homework
title: CSCI-UA.0480 - Homework #2
---

<div class="panel panel-default">
  <div class="panel-heading">Homework #2</div>
  <div class="panel-body" markdown="block">

# Higher Order Functions: Exercises and Processing Data - __Due xxxxx__

## Overview

### Description

__hoffy.js__ - Write a series of functions that demonstrate the use of the rest operator (or call/apply), and higher order functions

__restaurants.js__ and __report.js__ - Print out a report analyzing the NYC restaurants' health inspection ratings data.

### Submission Process

You will be given access to a private repository on GitHub. It will contain unit tests, stub files for your code, a `package.json` and a `.eslintrc`

* The final version of your assignment should be in GitHub.
* __Push__ your changes to the homework repository on GitHub.

### Minimum number of commits

As you write your code, make sure that you make at least four commits total (more commits are better; if you can, try to commit per feature added).

* the commits should be meaningful (that is, do not just add a newline, commit and push to make up the requirements for commits).
* make sure your commit messages describe the changes in the commit; for example:
  * add solutions to problem 2 and 3 of part 1
  * fix a bug that prevented reading of csv file

```
git add <files>
git commit -m 'your commit message'
```
* push your code frequently
```
git push
```

## Part 1 - Setup and Exercises

For this homework, you'll have files available in your repository, so you'll be cloning first.

The solutions to the following problems can go in the same file - __src/hoffy.js__:

### Setup

1. go to your github account...
2. find your repository: NetID-homework02 (note... this __should be your NetID__)
3. use the appropriate URL to run git clone

<pre><code data-trim contenteditable>git clone [YOUR REPO URL]</code></pre>

### Background Info

Implement functions that use JavaScript features such as:

* the rest operator
* the spread operator
* functions as arguments
* functions as return values
* decorators
* optionally call/apply/bind
* optionally arrow functions
* Array methods: 'filter', 'map', 'reduce'

Go through the functions in order; the concepts explored build off one-another, and the functions become more and more challenging to implement as you go on.

__Do not use__:

* `while` loops
* `for` loops
* `for ... in` loops
* `for ... of` loops
* `forEach` method .

__There will a small (-2) penalty every time one is used__. (Homework is 100 points total)


### Steps

1. prep...
    * create a `.gitignore` to ignore node_modules
	* create a `package.json` by using `npm init`
    * make sure that `mocha`, `chai`, and `eslint` are still installed (similar to previous assignment)
        <pre><code data-trim contenteditable>npm install -g mocha
npm install --save-dev eslint
npm install --save-dev chai
npm install --save-dev eslint-plugin-mocha
</code></pre>
    * you'll also need a few additional modules installed locally for the unit tests to run:
        * finally, install sinon and mocha-sinon locally for mocking `console.log` (these are for unit tests)
        * `npm install --save-dev sinon`
        * `npm install --save-dev mocha-sinon`
2. implement functions below in __hoffy.js__
3. make sure you export your functions as you implement them so that...
4. you can run tests as you develop these functions (again, the tests are included in the repository):
    `mocha tests/hoffy-test.js`
5. also remember to run eslint (there's a `.eslintrc` file included in the repository):
    `node_modules/.bin/eslint src/*`

### Functions to Implement

### (-2 per while, for, forEach, for of, or for in loop used)

<hr>

### `sum(num_1, num_2, ..., num_n)` - 3 points

__Parameters:__

* `num_1, num_2, ... num_n` - the values to be summed

__Returns:__

* the sum of the arguments as a `Number`
* if no arguments are passed in, give back `0`

__Description:__

Adds all of the arguments together and returns the resulting sum. If there are no arguments, the resulting sum is 0. Does not have to check for types.

HINTS:

* use `rest` parameters!

__Examples:__
```
// returns the sum of all arguments passed in
sum(1, 2, 3) // --> 6
sum(1, 1, 1, 1, 1, 1, 1, 1, 1, 1) // --> 10
sum(1) // --> 1

// returns 0 if there are no arguments passed in
sum() // --> 0
```
<hr>

### `findIndex(arr, num)` - 4 points

__Parameters:__

* `arr` - an `Array`
* `num` - a `Number` that we are looking for in the array 

__Returns:__

* an array of all indices of the number in the array [0 indexed]
* if the number is not in the array, return -1 (in an array)

__Examples:__

```
    findIndex([1, 2, 4, 3, 5], 2); // [1]
    findIndex([1, 2, 4, 3, 5], 8); // [-1]
    findIndex([1, 2, 4, 3, 2, 5, 3, 7, 2], 2); // [1, 4, 8]
```

<hr>

### `filterWith(fn)` - 4 points

__Parameters:__

* `fn` - a _callback_ function that takes in a single argument and returns a value (it will eventually operate on every element in an array)

__Returns:__

* `function` - a function that...
    * has 1 parameter, an `Array`
    * returns a new Array where only elements that cause `fn` to return `true` are present (all other elements from the old Array are not included)

__Description:__

This is different from regular filter. The regular version of filter immediately calls the callback function on every element in an Array to return a new Array of filtered elements. `filterWith`, on the other hand, gives back a function rather than executing the callback immediately (think of the difference between bind and call/apply). `filterWith` is basically a function that turns another function into a filtering function (a function that works on Arrays). 

__Example:__

    // original even function that works on Numbers
    function even(n) {return n % 2 === 0;} 

    // create a 'filter' version of the square function
    filterWithEven = filterWith(even); 

    // now square can work on Arrays of Numbers!
    console.log(filterWithEven([1, 2, 3, 4])); // [2, 4]    
    
    const nums = [1, NaN, 3, NaN, NaN, 6, 7];
    const filterNaN = filterWith(n => !isNaN(n));
    console.log(filterNaN(nums)); // [1, 3, 6, 7]

<hr>


### `makeSet(arr)` - 4 points

__Parameters:__

* `arr` - an `Array`

__Returns:__

* an array of just the unique elements in `arr`

__Description:__

A `Set` is a common data structure which only contains unique elements. In this problem, we want to convert any given array into a `Set`, this means we want to remove duplicates from the original array.

__Examples:__

```
    makeSet([1, 2, 2, 3, 1]); // [1, 2, 3]
    makeSet([1, 2, 4, 3, 5]); // [1, 2, 4, 3, 5]
    makeSet([1, 2, 4, 3, 2, 5, 3, 7, 2]); // [1, 2, 4, 3, 5, 7]
```

<hr>

### `intersection(arr1, arr2)` - 5 points

__Parameters:__

* `arr1` - the first array containing `Numbers`
* `arr2` - the second array containing `Numbers`

__Returns:__

* an `Array` containing the elements found in both `arr1` and `arr2`
* if there are no common elements, return an empty array.

__Description:__

Finding intersection of lists of data is a very common problem in CS. We only want to store the common elements from both arrays. If there are duplicates in any of the array then make sure that the resulting array only contains one instance of it.

__Hint:__

Converting the arrays to `sets` might be helpful.

__Examples:__

```
intersection([2], [2]); // [2]
intersection([2], [1]); // []
intersection([1, 2], [1]); // [1]
intersection([2, 1, 2], [1, 2]); // [1,]
```

<hr>

### `repeatCall(fn, n, arg)` - 5 points

__Parameters:__

* `fn` - the function to be called repeatedly
* `n` - the number of times to call function, `fn`
* `arg` - the argument to be passed to `fn`, when it is called

__Returns:__

* `undefined` (no return value)

__Description:__

This function demonstrates using functions as an argument or arguments to another function. It calls function, `fn`, `n` times, passing in the argument, `arg` to each invocation / call. It will ignore the return value of function calls. Note that it passes in only one `arg`.

__Examples:__

```
repeatCall(console.log, 2, "Hello!");
// prints out:
// Hello!
// Hello!

// calls console.log twice, each time passing in only the first argument

repeatCall(console.log, 2, "foo", "bar", "baz", "qux", "quxx", "corge");
    
// prints out (again, only 1st arg is passed in):
// foo 
// foo 
```

<hr>

### `constrainDecorator(fn, min, max)` - 5 points

__Parameters:__

* `fn` - the function to modify (_decorate_)
* `min` - the minimum value that `fn` can return
* `max` - the maximum value that `fn` can return

__Returns:__

* `function` - a function that...
    * does the same thing as the original function, `fn` (that is, it calls the original function)
    * accepts the same number of arguments as the original function, `fn`
    * the return value is the return value of `fn`, unless it is less than or greater than the `min` and `max`, in which case it returns `min` or `max` respectively

__Description:__

This function is a decorator. [See the slides on the decorator pattern](../slides/js/higher-order-functions-continued.html) for background information. It builds on top of the example in the slides by actually _modifying_ the return value of the original function.

This function wraps the function `fn` in another function so that operations can be performed before and after the original function `fn` is called. This can be used to modify incoming arguments, modify the return value, or do any other task before or after the function call. Again, we'll be modifying the return value in this case.

This particular decorator function constrains the result of the function being wrapped, `fn` so that its return value fits between `min` and `max` inclusive. If these are omitted from the original outer function, then the newly returned function will just return the value unmodified. You can assume that the return value of `fn` is `Number` (you do not have to deal with other types).


__Example:__

    // creates a new function from the built-in function, parseInt
    // the new function is the same thing as parseInt, but it constrains
    // the return value to a value between min and max (inclusive)
    const constrainedParseInt = constrainDecorator(parseInt, -10, 10);

    // still works like the original parseInt
    constrainedParseInt("7") // --> 7
    constrainedParseInt("-10")) // --> -10

    // but if the return value is less than min or greater than max
    // it returns min or max respectively
    constrainedParseInt("-12") // --> -10
    constrainedParseInt("12")) // --> 10

    // however, if either min or max are missing, then the new function
    // returns the result of fn unmodified regardless of value
    var constrainedParseInt2 = constrainDecorator(parseInt);
    constrainedParseInt2("-12") // --> -12

<hr>

### `limitCallsDecorator(fn, n)` - 6 points

__Parameters:__

* `fn` - the function to modify (_decorate_)
* `n` - the number of times that `fn` is allowed to be called

__Returns:__

* `function` - a function that...
    * does the same thing as the original function, `fn` (that is, it calls the original function)
    * but can only be called `n` times
    * after the `n`th call, the original function, `fn` will not be called, and the return value will always be `undefined`

__Description:__

This is the culmination of all of the concepts from the previous functions. However, instead of just reading from a variable that's available through the closure, you'll use it to keep track of the number of times that a function is called... and prevent the function from being called again if it goes over the `max` number of allowed function calls. Here are the steps you'll go through to implement this:

1. create your decorator (function)
2. create a local variable to keep track of the number of calls
3. create an inner function to return
    * the inner function will check if the number of calls is less than the max number of allowed calls
    * if it's still under max, call the function, `fn` (allow all arguments to be passed), return the return value of calling `fn`, and increment the number of calls
    * if it's over max, just return `undefined` immediately without calling the original function

__Example:__

    const = limitedParseInt = limitCallsDecorator(parseInt, 3);
    limitedParseInt("423") // --> 423
    limitedParseInt("423") // --> 423
    limitedParseInt("423") // --> 423
    limitedParseInt("423") // --> undefined


<hr>


### `compose(fn1, fn2, ...,fnN)` - 6 points

__Parameters:__

* `fn1, fn2, ..., fnN` - a bunch of functions

__Returns:__

* `function` - a function that will pass it's arguments to `fn1`, take the output of `fn1` and use it as the argument to `fn2`, then take the output of `fn2` and use it for `fn3`, and then... etc


__Description:__

A handy utility for automating the writing of code that's just calling functions to pass their arguments to other functions. You can assume that each function passed in only takes one argument.

HINT: we are _summing_ or _composing_ the functionality of a bunch of functions together

__Example:__


    // let's say you have some pretty procedural functions
    function superCamelCase(s) {
      return s
        .split("")
        .map((c, i) => (i % 2 == 0 ? c.toUpperCase() : c.toLowerCase()))
        .join("")
    }

    function spaceText(s) {
      return s.split("").join(" ")
    }

    function addStyle(s) {
      return "~~~ " + s + " ~~~"
    }

    // you want to make a playlist of them
    const aestheticFmtPipeline = compose(
      superCamelCase,
      spaceText,
      addStyle
    )

    console.log(aestheticFmtPipeline("hello world")) // ~~~ H e L l O   W o R l D ~~~

    function makeVertical(s) {
      return s.split("").join("\n")
    }

    // playlists of playlists of functions
    const tallAestheticFmt = compose(aestheticFmtPipeline, makeVertical)

    console.log(tallAestheticFmt("goodbye world"))
    /*
    ~
    ~
    ~

    G

    o

    O

    d

    B

    y

    E



    W

    o

    R

    l

    D

    ~
    ~
    ~
    */

### Test, Lint and Commit

Once you're finished with your functions, remember to:

1. make sure all tests are passing
2. make sure that eslint shows no errors
3. commit and push your code!


## Part 2 - Processing NYC Restaurant Examination Data

In this part, you'll work with a dataset of hygiene examination records of New York City restaurants.

The data is free to use as part of NYC's open data initiative.

You'll be using two files for this:
1. `restaurants.js` to create a function called `processRestaurantData`
    * the function will take an `Array` of objects with each object representing a listing
2. `report.js` to read in and parse JSON data and use the `processRestaurantData` function above to create a report

### Importing Data

* Download the data by going to [https://data.cityofnewyork.us/Health/DOHMH-New-York-City-Restaurant-Inspection-Results/43nn-pn8j-Results/43nn-pn8j](https://data.cityofnewyork.us/Health/DOHMH-New-York-City-Restaurant-Inspection-Results/43nn-pn8j) and clicking the "Export" button on the top right, then the "CSV" button.
    * place it in a folder outside of your repository
* Create `src/report.js`...
* Start by reading in the file (which should have a filename something like `DOHMH_New_York_City_Restaurant_Inspection_Results.csv`) (remember to uncompress the .gz file from above first) using `fs.readFile` (you can use the absolute path)
    * make sure that `fs` the module is brought in using `require`, then call the function)
    * __do not use `readFileSync`__
* See the docs on `fs.readFile` (hint: make sure you specify `utf8` as the second argument)
* The file that you read in contains reports of health inspections
    * there's one restaurant per line
    * each examination record is represented by a comma-delimited string
* Find a way to read in and parse the contents of the file so that:
    * leading and trailing white space is removed from the initial contents (use the [string method, `trim`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/trim))
    * each line into an actual JavaScript object, where the properties correspond with the first row of the file (the headers)
    * each resulting object is placed into an `Array` for later processing
    * you can check out some [String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) and  [Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array) documentation
    * note that the goal of this assignment is to work with higher order functions, so memory efficiency does not need to be taken into consideration
* All of your parsing can only be done from within the callback function (or the function to be called once data is read from the file) that you supply to `fs.readFile`
* Examine the resulting `Array` ... (for example, try printing it out!)
* Later, you will be supplying this `Array` to the `processBiteData` function that you create in `bitefunc.js` to generate a report.
* __You only need to use the following columns from the data (disregard the rest)__
  * CAMIS (Unique ID)
  * DBA (Name of the restaurant)
  * Zipcode
  * Cuisine Description
  * Inspection Date
  * Score
  * Grade
* To verify your file reading and parsing, you can try:
  printing the "boro", "DBA", "score", "grade" of the 2nd (remember the array index starts from 0) listing in the file in the format: '${bizz.DBA} in ${bizz.boro} has a health inspection score of ${bizz.score} with a grade ${bizz.grade}.'
```
Sushi Yu in Brooklyn has a health inspection score of 10 with a grade A.
```

### Examining the Data
* Assuming that your parsed data is in a variable called `data` ...
* `data` will be an `Array` of JSON objects (each line should have been parsed from JSON before pushing into the `data` array)
* Each object in `data` contains location data, score, grade, and categories.

Below is a sample listing from the dataset with a description of properties you'd need for your assignment

```
{
  // nyc's integer id for this restaurant
  "CAMIS": 41615149,

  // name of the restaurant
  "DBA": "GOLDEN STARS PIZZA",

  // borough
  "boro": "Brooklyn",

  // integer zipcode
  "zipcode": 11204,

  // cuisine description
  "cuisine": "Italian",

  // inspection date
  "date": "10/28/2019",

  // Integer Score
  "score": 13,

  // Grade
  "grade": "A"
}
```


### Analytics

#### The `processRestaurantData` Function

You'll create a function to generate a report (as a string) based on the health inspection data. You'll write this function in `restaurant.js`.

### `processRestaurantData(restaurants)`

__Parameters:__

* `restaurants` - an `Array` of objects, with each object representing a report of an inspection

__Returns:__

* a string containing a report based on the data passed in

__Description:__

This function will generate a report based on the `Array` of objects passed in. The report will contain answers to some questions based on the data.

__Important note about parsing numerical values:__

One of the most common peculiarities you'll come across while working with datasets is that the values read in from a file is that they might not be in the format you expect them to be (they may not be the _right_ type).

 eg. you might see

 ```
 "age": "5"
 ```

It's actually a string whereas we'd like to use it as a float value.

In situations like these, you'll need to parse the numerical value from the string. Here, we'll [use the `parseInt(strval)` function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseInt)


### Implementation Requirements

1. When creating your report in `processRestaurantsData`, you must use all of the following Array methods at least once each in your program:
    * `forEach`
    * `filter`
    * `map`
    * `reduce`
    * There will be a small penalty for each one not used (-2).
    * HINT: A typical pattern is to always use map 99% of the time, so you never accidentally get rid of or mess up the data, except when you're doing your first pass through the data to clean it up. 
	
### Report Overview

Your report will use the data passed in to determine:

1. Average score of restaurants in Staten Island and Bronx.
2. The most frequent grade for restaurants in Brooklyn.
3. Boroughs ranked by most number of A grades.
4. What percentage of restaurants in Queens are Chinese restaurants?
5. Top 3 restaurants in Manhattan with the lowest score value. (low scores are better)

See the following details...

### Average Score

* Include the average score of all the restaurants in the file but only belonging to first Staten Island, and then the Bronx; format to have at least two decimal places. Example output below:

```
Average score of restaurants in Staten Island: 17.21
Average score of restaurants in the Bronx: 15.21
```

* Be careful of weird things popping up in the score column! You can disregard empty values and values <= 0. Don't worry if your number is slightly different.


### Most frequent grade in Brooklyn

* Go through each restaurant in Brooklyn and note which grade occurs the most number of times.

```
The most frequently occuring grade in Brooklyn is A!
```

### Boroughs ranked by A grades

* Rank each borough by the number of A grades

```
1. Brooklyn has 94 A grades
2. Manhattan has 68 A grades
3. Queens has 59 A grades
4. Bronx has 42 A grades
5. Staten Island has 21 A grades
```

### Percentage of Chinese restaurants in Queens

* Find what % of all restaurants in Queens are Chinese restaurants. Check that the Cuisine is "Chinese"; format to have at least two decimal places. Example output below:

```
Of all the restaurants in Queens, 17.33% are Chinese restaurants.
```

### Top three restaurants in Manhattan with lowest rating

* Go through each restaurant in Manhattan and find the ones with the lowest rating and show the best 3. Example output:
  
```
The best restaurants in Manhattan are:
1. Bubba Gump Shrimp Co.
2. Halal Guys.
3. Olive Garden.
```
(actual results might be different, these are examples)

### Return Value

All of the analytics should be coalesced into a single large string representing the analytic report.

This string should be returned by your `processRestaurantsData` function in your module, `restaurants.js`

### Calling processBiteData

Now that you've finished your function, you can try calling it on your data from `report.js`

1. In report.js: require the module that you created (`restaurants.js`).
2. Use your function on the data that you parsed from reading in the `DOHMH_New_York_City_Restaurant_Inspection_Results.csv` file that you opened earlier.
3. Print out the resulting string.
4. You can compare your output with the example output below

```
Average score of restaurants in Staten Island: 17.21
Average score of restaurants in the Bronx: 15.21

The most frequently occuring grade in Brooklyn is A!

Boroughs ranked by A grades:
1. Brooklyn has 94 A grades
2. Manhattan has 68 A grades
3. Queens has 59 A grades
4. Bronx has 42 A grades
5. Staten Island has 21 A grades

Of all the restaurants in Queens, 17.33% are Chinese restaurants.

The best restaurants in Manhattan are:
1. Bubba Gump Shrimp Co.
2. Halal Guys.
3. Olive Garden.
```

Lint, commit and push your code.
</div>

</div>