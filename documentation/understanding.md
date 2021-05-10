# The understanding

The definition of the [cognitive complexity](./cognitive-complexity.md) uses the word `understand`. We need to accurate what we mean when we use this term. In other words, we need to precise what are the attributes of what we call *"understanding"*, how they are correlated to the cognitive complexity, and how we could measure them in the real world.

At first, our goal is not to define what is *understanding* in all the situations where this word can be used, but only in the context of the *software understanding*. Our aim is to define the *understanding* relatively to a [code snippet](code-snippets.md), not in other situations.

## Table of contents

* [Where is the problem ?](#where-is-the-problem-)
* [Understanding of imported references](#understanding-of-imported-references)
* [Understanding of valid code snippets](#understanding-of-valid-code-snippets)
* [Minimal cognitive complexity](#minimal-cognitive-complexity)
* [Refactoring](#refactoring)
    * [Definition of refactoring](#definition-of-refactoring)
    * [Simplifications](#simplifications)    

## Where is the problem ?

Let's begin by a simple example. 

```ts
// Code snippet s

function multiplyByTwo(a: number): number {
	return a * 2;
}
```

What means exactly to *understand* this code snippet ? Is it to understand what is the ***role*** of the function `multiplyByTwo` ? In this case, you only need to look at its name : this function will simply multiply a number by two, that's all. You don't need to look at what is *inside* the function. At the opposite, we could say that you *understand* this method if you understand *how* this method will return `a` multiplied by two. It seems that we could have two different definitions of the word *understand*. 

In reality, the two kinds of definitions are interesting. In the first one, we say that a developer understands the ***signified*** of the written instructions, and in the other case we say that he understands the ***significant*** of these instructions, *i.e.* what means every word of the code snippet.

## Understanding of imported references

> **Definition**
>
> A developer ***understands the role of an imported reference*** `r` located in a code snippet `s` if he is able to predict, when a process calls `r`, the same [behavior of the system](systems.md) than the author of the implementation of `r` would predict.

**Remark**

This definition doesn't mean that a developer understands an imported reference `r` when he is able to predict the behavior of the system when a process calls `r`, but that he is able to do the *same predictions* that the author of the imported references would do in the same circumstances.

> **Definition**
>
> The ***cognitive complexity of an imported reference*** `r` located in a given snippet `s` is the time needed by a mean developer to predict the behavior of the system when this reference will be called by a given process `p`.
> 
> The ***cognitive complexity of an exported reference*** `r` located in a given snippet `s` is the time needed by a mean developer which will import this reference to predict the behavior of the system when this reference will be called by a given process `p`.

## Understanding of valid code snippets

> **Definition**
>
> A developer ***understands a context-sensitive valid code snippet*** `s` if :
> 1. he understands the role of each of the [exported references](code-snippets-tmp.md#behaviors-roles-and-descriptions) of `s`.
> 2. he understands the role of each of its [imported references](code-snippets-tmp.md#basic-definitions-around-code-snippets) located in `s`.
> 3. assuming that the behavior of the imported references of `s` corresponds to their roles, he is able to predict the behavior of the exported references of `s`.

* Example

```ts
// Code snippet s
function getBill(article: Article): number {
	const price: number = article.getPrice();
	const vat: number = VAT_RATE * price;
	return price + vat;
}
```

A developer *understands* `s` if :

*1. Role of exported references*

- he understands that `s` represents a function called `getBill()` which takes an `Article` in parameter, and that its role is to return the bill of a given article.
    
*2. Role of imported references*

- he understands that `getPrice()` is a method of the class `Article` which will return the price of the article.
- he understands that `VAT_RATE` is the vat rate to use.
  
*3. Behavior of the external references*

- he predicts that the behavior of `getBill()` is correct, *i.e.* that its returned value will really be the price of the article including the vat.

**Remark**

With this definition, a developer may understand `s` even if `getBill()` will return a value which will not be correct, *i.e.* which will not be the price including VAT of a given article. He is only able to predict that *if there is no bug in the implementation of the imported references of `s`*, *i.e.* if their behavior corresponds to their role. 

This is not in contradiction with the intuitive notion of code understanding: with the definition above, if a developer understands `s`, he will be able to detect that its real behavior is not what he expected, *i.e.* he will detect a bug, which is probably what we mean when we say that a developer understands a code snippet: he is able to debug it.

[-> Top](#the-understanding)
## Minimal cognitive complexity

> **Definition**
> 
> Let `s` a context-sensitive valid code snippet and `b` its behavior.
> The ***minimal cognitive complexity*** of `b` is the lower limit of the cognitive complexities of the set of code snippets having collectively the same behavior as `b`.
> 
> We note it `minCc(s)`.

* Example

```ts
// Code snippet s
function getProfile(id: number): Profile {
  if(isClientId(id)) {
    // Do some long stuff returning the profile of the client corresponding to the given id
  } else {
    // Do some long stuff returning the profile of a company corresponding to the given id
  }
}
```

```ts
// Code snippet t
function getProfile(id: number): Profile {
  return isClientId(id) ? getClientProfile(id) : getCompanyProfile(id);
}

function getClientProfile(id: number): Profile {
  // Do some long stuff returning the profile of the client corresponding to the given id
}

function getCompanyProfile(id: number): Profile {
	// Do some long stuff returning the profile of a company corresponding to the given id
}
```

`s` and `t` are two different elements of **V**<sup>+</sup> having the same behavior. Assuming that `Cc(t) < Cc(s)` we have `minCc(s) < Cc(t) < Cc(s)`. Please note that, by construction, `minCc(s) = minCc(t)`.

[-> Top](#the-understanding)
## Refactoring

### Definition of refactoring

> **Definition**
>
> A ***modification*** of a code snippet is an operation from **S** to **S** which assigns to a code snippet `s` a code snippet `t` different from `s`.

> **Definition**
> 
> A ***refactoring*** is a *modification* which assigns to a context-sensitive valid code snippet `s` a set of context-sensitive valid code snippets *t<sub>1</sub>, ... t<sub>n</sub>* which collectively have the same behavior as `s`. The refactoring is an operation from **[V<sup>+</sup>](code-snippets-tmp.md#valid-code-snippets)** to **V**<sup>+<sup>n</sup></sup>.
> 
> *r: (s ∈ V<sup>+</sup>) -> (t<sub>1</sub>, ... t<sub>n</sub> ∈ V<sup>+<sup>n</sup></sup>)*
> 
> By extension, the refactoring of a feature is the action to transform a feature `f` in a feature `g` which provides the same functionalities to the users.


### Simplifications

> **Definition**
>
> A ***simplification*** of a valid code snippet `s` is a refactoring `r` as `c(r(s)) < c(s)`, where `c` is the cognitive complexity metric. We say that `s` was ***simplified***.

> **Proposition**
> 
> Some code snippets may be simplified.

**Demonstration**

Let `s` the code snippet below:

```ts
// Code snippet s
if (a > 0) { return; }
if (a > 0) { return; }
```
The second line is a dead code, so we can remove it without changing the behavior of the program.

```ts
// Code snippet s'
if (a > 0) { return; }
```

The role of `s'` is the same as `s`, so the operation `r: s -> s'` is a refactoring. The second line of `s` was not empty, and any non-empty code snippet is strictly higher than 0. Thus, by removing the second line of `s`, we decreased its cognitive complexity. If we call `c` the cognitive complexity metric, we have

`c(r(s)) < c(s)`

This example demonstrates that a refactoring may decrease the cognitive complexity of a code snippet. 

We can now try to find useful [simplification technics](simplification-technics.md).

## Refactoring technics

In the aim to increase software maintainability by decreasing cognitive complexity, the developers will use many refactoring technics. Some of them are efficient, but others are probably not. There is a high probability that sometimes, the refactoring operations are increasing the cognitive complexity instead of decrease it. Some technics are efficient in any cases, and others only in some specific situations.

### Remove the dead code

> **Proposition**
>
> The refactoring which consists of removing the dead code is a simplification.

> *Demonstration*
> 
> Let `s` a context-sensitive valid code snippet.
> 1. The action consisting of remove the dead code of `s` is a refactoring because it doesn't change its behavior. 
> 2. Any non-empty code snippet has a cognitive complexity strictly higher than 0. 
> With 1. and 2., we can assert that this action is a simplification.

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

The developer which reads this code snippet must read all the lines to understand the [role](code-snippets-tmp.md#roles) of the function `f`. By adding a simple line of comment, he can clarify this role, and thus decrease dramatically the cognitive complexity of this code snippet:

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
