# tutorials
## More on Functions

#### Function with same name overrides the previous (defined in the same context)

> see below and guess the output

```javascript
function foo(a){
	console.log('1');
}
function foo(a,b){
	console.log('2');
}
function foo(a,b,c){
	console.log('3');
}
foo(1);
foo(1,2);
foo(1,2,3);
```
> output

```javascript
>3
>3
>3
```

> You can also try like below

```javascript
function foo(a){
	console.log('1');
}
foo(1);

function foo(a,b){
	console.log('2');
}
foo(1,2);


function foo(a,b,c){
	console.log('3');
}
foo(1,2,3);

```

> but the output will be same as above due to JavaScript Hoisting

```javascript
>3
>3
>3
```
#### Avoid the overriding using the closures

```javascript
(function(){	
	function foo(a){
		console.log('1');
	}
	foo(1);	
}());

(function(){	
	function foo(a,b){
		console.log('2');
	}
	foo(1,2);	
}());

(function(){	
	function foo(a,b,c){
		console.log('3');
	}
	foo(1,2,3);	
}());
```
> output

```javascript
>1
>2
>3
```

####Parameters and Arguments Object

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









