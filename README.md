# tutorials

##Functions
### Function declaration and Function expression(literal) notation.

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
in either ways, 
the name `foo` will be avalable in the context where it is diclared and it will refer the function definition.

##### Name Collission
either you choose declaration style or literal notation, if you use the same name again with in the context, the name will refer the latest definition that is diclared.
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

######The uncommon behaviour between diclarative and literal notations
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
This unpredictable behaviour is due to *Hoisting*.

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
>so it is advisable to use literal notation over diclaration style to avoid unpredicable behaviour due to hoising.

###Parameters and Arguments Object
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


### Higher Order functions
since a function reference can be passed as an argument parameter, it is possible to compose higher order functions.

###### Array traversing
```javascript
var data=[{name:'testuser1',age:20},{name:'testuser2',age:23},{name:'testuser3',age:30}];
for(var i in data){
	console.log(i, data[i]);
}
```
>output 
```javascript
0 Object {name: "testuser1", age: 20}
1 Object {name: "testuser2", age: 23}
2 Object {name: "testuser3", age: 30}
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


####### Now combining above concepts and implimenting a higher order function `foreach` 
```javascript
	var foreach = function(data, iterator){
		for(var i in data){
			//console.log(i, data[i]);
			iterator(i,data[i]);
		}
	}
	
	//usage
	foreach(data,function(i,record){
		console.log(i, record, record.name);
	});
```
>output 
```javascript
0 Object {name: "testuser1", age: 20}
1 Object {name: "testuser2", age: 23}
2 Object {name: "testuser3", age: 30}
```








