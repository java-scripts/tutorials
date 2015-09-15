# tutorials

##Functions

whether you declare a function like below
```javascript
function foo(){
	console.log('foo');
}
```
or using the literal notation like below
```javascript
var foo = function(){
	console.log('foo');
}
```
in either ways, 

the name `foo` will be avalable in the context where it is diclared and it will refer the function definition.

#### Name Collission
```javascript
function foo(){
	console.log(1);
}
function foo(){
	console.log(2);
}
foo()
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
>2
>2
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


