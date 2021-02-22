# Infix Function Composition in JS
Exploring the possibilities--particularly what can be done natively with JS as it sits right now.

## Overloading `Object`'s `.` property accessor
As seen here in [Haskell-like composition in JavaScript](https://medium.com/@nikogosovd/haskell-like-composition-in-javascript-3624fcfca19b)
```
const composable = {
	get: function(target, prop) {
		if (prop in target) {
			return target[prop]
		}
		
		const entity = eval(prop);
		if (typeof entity === 'function' && typeof target === 'function') {
			return new Proxy(
				(...args) => target(entity(...args)),
				composable
			)
		}
	}
}


const id = new Proxy(x => x, composable)
```

This approach fails to meet several requirements. First, as stated in the article:
1. It requires a first function to kick off the `Proxy`ing of the following functions' accessors to a compose operation.
2. Anonymous functions don't work unless wrapped in an Array and the syntax gets weird because you then skip the `.` altogether.
3. It, "doesn’t support anonymous functions with free variables that are not in the same scope as the getter trap." I'm not even clear on the scenario that describes.
```
const greet = name => `Hello, ${name}.`
const exclaim = expression => expression.replace('.', '!')

// Define screamGreeting where:
// screamGreeting('Liz') === 'HELLO, LIZ!'

// Works
const screamGreeting = id [x => x.toUpperCase()] . exclaim . greet

// Doesn't
const screamGreeting = id . function(x){ return x.toUpperCase() } . exclaim . greet
// -> Uncaught SyntaxError: Unexpected token {
```

It also breaks when using idomatic syntax such as accessing functions from other objects (this one is obvious, so perhaps forgivable), evaluating expressions within `()` or calling a function (which would necessarily need to return a function).
```
// Doesn't work, but Ok...
const screamGreeting = id . _.upperCase . exclaim . greet
// -> Uncaught ReferenceError: upperCase is not defined

// These break idiomatic JS, right? :(
const screamGreeting = id . (_.upperCase) . exclaim . greet
// -> Uncaught SyntaxError: Unexpected token (
const sayMultipleTimes = x => expression => Array(x).fill(expression).join(' ')
const greetThrice = id . sayMultipleTimes(3) . greet
// -> Uncaught TypeError: greetThrice is not a function
```

## Other Ideas?
Is it possible to overload `+`? Probably not, and it would be a breaking change since adding two functions currenlty results in type coercion (i.e. `toString()`) and concatenation.

What about overloading `<<` && `>>`? This can [definitely be done](https://2ality.com/2011/12/fake-operator-overloading.html), but can it be harnessed for composition?
