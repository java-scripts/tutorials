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
foo()
```
> output
```javascript
> 2
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
so it is advisable to use literal notation over diclaration style to avoid unpredicable behaviour due to hoising.

