# Simplifications technics

In the aim to increase software maintainability by decreasing cognitive complexity, the developers will use many refactoring technics. Some of them are efficient, but others are probably not. There is a high probability that sometimes, the refactoring operations are increasing the cognitive complexity instead of decrease it. Some technics are efficient in any cases, and others only in some specific situations.

The aim of this page is to study the impact of the different [refactoring technics](understanding.md#simplifications) on the value of the Cognitive Complexity.

### Remove the dead code

> **Proposition**
>
> The refactoring which consists of removing the dead code is a simplification.

> *Demonstration*
>
> Let `s` a context-sensitive valid code snippet.
> 1. The action consisting of remove the dead code of `s` is a refactoring because it doesn't change its behavior.
> 2. Any non-empty code snippet has a cognitive complexity strictly higher than 0.
     > With 1. and 2., we can assert that the removing of the dead code is a simplification.


### Clarify identifiers

> **Conjecture**
>
> If `s` is a valid code snippet containing a given identifier `i`, the action to rename `i` may be a simplification.

* Example

```ts
// Code snippet s
function f(a: number): number {
	return a * 2;
}

// Code snippet s'
function multiplyByTwo(a: number): number {
	return a * 2;
}
```

Even if we can't demonstrate this conjecture without experiments, we can say without risks that the cognitive complexity of `s'` is lower than the cognitive complexity of `s`.

### Add comments

> **Conjecture**
>
> Let `r` a refactoring consisting of adding comments, and `s` a given context-sensitive valid code snippet.
> `r` may decrease or increase the cognitive complexity of `s`.

* Example 1

```ts
// Code snippet s
function f(o, v) {
	let p = 0;
	for (let a of o.articles) {
		p = p + a.price;
    }
	p = p * v;
    return p;
}
```

The developer which reads this code snippet must read all the lines to understand the [role](code-snippets-tmp.md#behaviors-roles-and-descriptions) of the function `f`. Moreover, he must find some code snippets importing `f` to be able to understand that the meaning of the parameter `v` is the VAT. 

By adding some comments, he can clarify the role of `f`, and thus decrease dramatically its cognitive complexity:

```ts
// Code snippet r(s)

// Returns the price including VAT of a set of articles
// @param o     // The order with articles
// @param v     // The current VAT rate
function f(o, v) {
	let p = 0;
	for (let a of o.articles) {
		p = p + a.price;
    }
	p = p * v;
    return p;
}
```


* Example 2

```ts
// Code snippet s
function multiplyByTwo(a: number): number {
	
}
```

### Type the code


### Split the code in smaller parts


### Reduce the number of lines of code


> **Conjecture**
>
> Let `r` a refactoring consisting of removing line breaks, and `s` a given context-sensitive valid code snippet.
> `r` may decrease or increase the cognitive complexity of `s`.

* Example 1

```ts
// Code snippet s
if (a > 0) {
	return 1;
} else {
	return 2;
}

// Code snippet r(s)
if (a > 0) { return 1; } else { return 2; }
```

It is usually recommended implementing this algorithm by using the form of `s` instead of the form of `r(s)`, for questions of readability. It is probably true that the initial form of `s` is more easy to read, and so easier to understand. We can conjecture that `cc(s) < cc(r(s))`, thus `r` is probably not a simplification.

* Example 2

```ts
// Code snippet s
return a > 0
  ? 1
  : 2;

// Code snippet r(s)
return a > 0 ? 1 : 2;
```

The ternary operations which are short are usually written in one line, for questions of readability. If it is true (and that's probably the case), `r` is a simplification.

***Work in progress...***
