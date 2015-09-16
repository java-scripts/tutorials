#More Into Functions

---

* Functions
  * Function declaration and Function expression (literal) notation.
  * Name Collision
  * The uncommon behavior between declarative and literal notations
  * Parameters and Arguments Object
* Higher Order functions
* Functional Style
  * Map, Reduce & Currying
* Asynchronous Style
* Closures and IIFE

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
### Map, Reduce & Currying
# Asynchronous Style
# Closures and IIFE
