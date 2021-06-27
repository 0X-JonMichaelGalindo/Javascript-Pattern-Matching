# Javascript-Pattern-Matching

Pattern matching is a concise, easy-to-read syntax for writing functions whose computation depends on the type of parameter past.

# Example #1

Computing a fibonacci number via recursive pattern matching.

```javascript
const fib = n => ( {

    [ n === 0 ] : n => 0 ,
    [ n === 1 ] : n => 1 ,
    [  n > 1  ] : n => fib( n - 1 ) + fib( n - 2 ) ,
    
}[ true ]( n ) );

console.log( fib( 10 ) ); //logs: 55
```

# Example #2

Handling a mouse event.

## expression based

```javascript

let x , y , isClicking;

const handle = ev => ( {

  [ ev.type === 'mousedown' ] : () => isClicking = true ,
  [ ev.type === 'mousemove' ] : ev => ( x = ev.offsetX , y = ev.offsetY ) ,
  [  ev.type === 'mouseup'  ] : () => isClicking = false ,

}[ true ]( ev ) );

```

## match based

```javascript

let x , y , isClicking;

const handle = ev => ( {

  [ 'mousedown' ] : () => isClicking = true ,
  [ 'mousemove' ] : ev => ( x = ev.offsetX , y = ev.offsetY ) ,
  [  'mouseup'  ] : () => isClicking = false ,

}[ ev.type ]( ev ) );

```

# Explanation

In a javascript object initialization, identical subsequent [computed property names](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer#computed_property_names), repeatedly overwrite the same property.

```javascript
const a = { [true]:1, [true]:2, [true]:3 };

//a is { 'true':3 }
```

By storing booleans as property names, then accessing a boolean, we succinctly select 1 value corresponding to the last matching expression.

```javascript
const a = { [true]:1, [true]:2, [true]:3 };

//a is { 'true':3 }

console.log( a[ true ] ); //logs: 3
```

We wrap this succinct selection in a function for reusability, and compute the boolean property names from the functions parameters.

This provides syntactically clear pattern matching.

```javascript

const sign = n => ( {

  [  n < 0  ] : - 1 ,
  [ n === 0 ] :   0 ,
  [  n > 0  ] : + 1 ,
  
}[ true ] );

console.log( sign( -0.5 ) ); //logs: -1

```

By storing [arrow functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions) as values, we select 1 function corresponding to the last true expression.

By calling that function immediately, our matching function returns a selected computation result.

Arriving at our original example.

```javascript
const fib = n => ( {

    [ n === 0 ] : n => 0 ,
    [ n === 1 ] : n => 1 ,
    [  n > 1  ] : n => fib( n - 1 ) + fib( n - 2 ) ,
    
}[ true ]( n ) );

console.log( fib( 10 ) ); //logs: 55
```

# Installation

Install an up-to-date browser on your platform of choice. Modern browsers support arrow functions and computed property names.

# Usage

The syntax provided here works well, but may be varied to your personal taste.

For example, the fibonacci example might use matching rather than expression evaluation:

```javascript
const fib = n => ( {

    [ n ] : n => fib( n - 1 ) + fib( n - 2 ) ,
    [ 1 ] : n => 1 ,
    [ 0 ] : n => 0 ,
    
}[ n ]( n ) );

console.log( fib( 10 ) ); //logs: 55
```
