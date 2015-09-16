#More Into Functions

---

* Functions
  * [Function declaration and Function expression (literal) notation.](#function-declaration-and-function-expression-literal-notation)
  * [Name Collision](#name-collision)
  * [The uncommon behavior between declarative and literal notations](#the-uncommon-behavior-between-declarative-and-literal-notations)
  * [Parameters and Arguments Object](#parameters-and-arguments-object)
* [Higher Order functions](#higher-order-functions)
* [Functional Style](#functional-style)
  * [Map, Reduce & Currying](#map-reduce--currying)
* [Asynchronous Style](#asynchronous-style)
* [Closures and IIFE](#closures-and-iife)

 ---
 
# Functions
### Function declaration and Function expression (literal) notation.
Function declaration
```javascript
function foo(){
	console.log('foo');
}
```
Function literal notation
```javascript
var foo = function(){
	console.log('foo');
}
```
in either ways, the name `foo` will be available in the context where it is declared and it will refer the function definition.

### Name Collision
 
 either you choose declaration style or literal notation, if you use the same name again within the context, the name will refer the latest definition that is declared.
```javascript
function foo(){
	console.log(1);
}
function foo(){
	console.log(2);
}
foo();
```
> output
```javascript
>2
```

### The uncommon behavior between declarative and literal notations
```javascript
function foo(){
	console.log(1);
}
foo();
function foo(){
	console.log(2);
}
foo();
```
>output
```javascript
> 2
> 2
```

This unpredictable behavior is due to *Hoisting*.

using literal notation
```javascript
var foo = function(){
	console.log(1);
};
foo();
var foo = function(){
	console.log(2);
};
foo();
```
>output
```javascript
>1
>2
```
>so it is advisable to use literal notation over declaration style to avoid such unpredictable behavior.




### Parameters and Arguments Object
```javascript
function add(a,b){
	return a+b;
}

add(1);
add(1,2);
add(1,2,3);
```
> output

```javascript
>NAN
>3
>3
```
#####Arguments Object

what datatypes can we use as parameters? 

>you are free to use any

```javascript
function foo(){	
	for(var i in arguments){
		console.log(arguments[i], typeof arguments[i])
	}
}

foo(1, '2', true, [], {}, function(){} );
```

> output

```javascript
>1 "number"
>2 string
>true "boolean"
>[] "object"
>Object {} "object"
>function(){} "function"
```
also try  

```javascript
foo(undefined, null, NaN, Infinity); 
```

# Higher Order functions
since a function reference can be passed as an argument parameter, it is possible to compose higher order functions.

###### Array traversing
```javascript
var data = [{label:'A',value:11},{label:'B',value:22},{label:'C',value:33}];
for(var i in data){
	console.log(i, data[i]);
}
```
>output 
```javascript
>0 Object {label: "A", value: 11}
>1 Object {label: "B", value: 22}
>2 Object {label: "C", value: 33}
```
###### passing function as an argument

```javascript
var foo = function (callback){
	callback();
}
//
foo(function(){
	console.log('callback is invoked...');
});
```
> output
```javascript
callback is invoked...
```


######Now combining above concepts and implementing a higher order function `foreach` 
```javascript
	var foreach = function(data, iterator){
		for(var i in data){
			//console.log(i, data[i]);
			iterator(i,data[i]);
		}
	}
	
	//usage
	foreach(data,function(i,record){
		console.log(i, record);
	});
```
>output 
```javascript
0 Object {label: "A", value: 11}
1 Object {label: "B", value: 22}
2 Object {label: "C", value: 33}
```


# Functional Style
Writing the code in Declarative Style.
Involves deriving new functions out of existing functions.
```javascript
var sumofSquaresFn = pipeFn(squaresFn,sumFn);
sumofSquaresFn([1,2,3]) //output should be 14
```



### Map, Reduce & Currying

Defining Map function
```javascript
var map = function(mappingFn,data){
	var results=[];
	for(var key in data){		
		results.push(mappingFn(data[key],key));
	}
	return results;		
}
//define a square function
var square = function(v){return v*v;};
//testing the map with square function
console.log('squares of [1,2,3] =',map(square,[1,2,3]));
```
>output

```javascript
squares of [1,2,3] = [1, 4, 9]
```

Defining Reduce function
```javascript
var reduce = function(reducingFn,data){
	var memo = data[0];
	for(var index=1;index<data.length;index++){					
		memo = reducingFn(memo,data[index]);		
	}
	return memo;	
}
//define add function 
var add = function(a,b){return a+b;};

//testing the reduce with add function
console.log('sum of [1,2,3] =',reduce(add,[1,2,3]));
```
>output
```javascript
>sum of [1,2,3] = 6
```


Defining Curry Function. Is a partial function composed out of existing function with less number of arguments.
In the above example the map function requires two arguments(mappingFn,data). 
I want a curried function out of map with mappingFn. 
I will reuse this curried function in later point of time supplying the data alone.
 

```javascript
var curry = function(fn,arg1){
	return function(arg2){
		return fn(arg1,arg2);
	}
}

//usage
var squares = curry(map,square);
var sum = curry(reduce, add);

//tests
console.log('squares of [1,2,3] =',squares([1,2,3]));
console.log('sum of [1,2,3] =',sum([1,2,3]));
```

Define another function which pipes the result 

```javascript
var pipe = function(f1,f2){
	return function(data){
		return f2(f1(data));
	}
}
```
Now everything we need is done. test the below

```javascript
//usage
var sumofSquares = pipe(squares,sum);
//test
console.log('sumOfSquare of [1,2,3] =', sumofSquares([1,2,3]));
```


# Asynchronous Style
# Closures and IIFE
