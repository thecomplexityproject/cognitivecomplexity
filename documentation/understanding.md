# The understanding

The definition of the [cognitive complexity](./cognitive-complexity.md) uses the word `understand`. We need to accurate what we mean when we use this term. In other words, we need to precise what are the attributes of what we call *"understanding"*, how they are correlated to the cognitive complexity, and how we could measure them in the real world.

At first, our goal is not to define what is *understanding* in all the situations where this word can be used, but only in the context of the *software understanding*. Our aim is to define the *understanding* relatively to a [code snippet](code-snippets.md), not in other situations.

## Table of contents

* [Role and behavior](#role-and-behavior)
* [Understanding of references](#understanding-of-references)
* [Understanding of valid code snippets](#understanding-of-valid-code-snippets)
* [Minimal cognitive complexity](#minimal-cognitive-complexity)
* [Refactoring](#refactoring)
    * [Definition of refactoring](#definition-of-refactoring)
    * [Simplifications](#simplifications)    

## Role and behavior

Let's start with a simple example. 

```ts
// Code snippet s

function multiplyByTwo(a: number): number {
	return a * 2;
}
```

To define the word *understand* in the definition of the cognitive complexity, we could simply say: *a developer understands the function `multiplyByTwo()` if he is able to predict that the value returned by this function will be equal to the value of the parameter `a` multiplied by two. In other words, we could say something like *"a developer understands `multiplyByTwo()` if he understands its implementation"*. Unfortunately, this is not enough to describe what we intuitively mean by *"understand"*. Let's look at the example below.

```ts
// Code snippet t

function multiplyByTwo(a: number): number {
  return a * 3;
}
```

If the developer understands the implementation, *i.e.* that this method will return a number multiplied by 3, but don't understand that there is a contradiction with the *name* of the function, should we say that he really understood this code snippet ? Surely not. A developer understands a function if he is able to predict its *expected behavior* and its *real behavior*.

The name of the function `multiplyByTwo()` clearly indicate that its *role* is to return a number multiplied by two. Its *implementation* is correct, because the *behavior of the system* will be as expected, *i.e.* will return the number multiplied by 2.

A developer really understands this function if he is able to understand its *role*, and if he is able to predict that its *implementation* is correct.  

## Understanding of references

> **Definition**
>
> A developer ***understands the role of an external reference*** `r` if he is able to predict, without the help of the implementation of `r`, the [behavior of the system](systems.md) when `r` is called by a given code snippet.
>
> A developer ***understands the implementation of an external reference*** `r` if he is able to predict, without the help of the description of `r`, the [behavior of the system](systems.md) when `r` is called by a given code snippet.

> **Definition**
>
> A developer ***understands an external reference*** `r` if he is able to predict if there is a bug in the implementation of `r`.

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
> 1. he understands the role of each [exported reference](code-snippets-tmp.md#references) of `s`.
> 2. he understands the role of each [imported reference](code-snippets-tmp.md#references) located in `s`.
> 3. assuming that the behavior of the imported references of `s` corresponds to their roles, he is able to predict the behavior of the exported references of `s`.

* Example

```ts
// Code snippet s
function getPriceWithVat(article: Article): number {
	const price: number = article.getPrice();
	const vat: number = VAT_RATE * price;
	return price + vat;
}
```

A developer *understands* `s` if :

*1. Role of exported references*

- he understands that `s` represents a function called `getPriceWithVat()` which takes an `Article` in parameter, and that its role is to return the price including VAT of a given article.
    
*2. Role of imported references*

- he understands that `getPrice()` is a method of the class `Article` which will return the pre-tax price of the article.
- he understands that `VAT_RATE` is the vat rate to use.
  
*3. Behavior of the external references*

- he predicts that the behavior of `getPriceWithVat()` is correct, *i.e.* that if the external references `getPrice()` and `VAT_RATE` are correctly implemented, the value returned by `getPriceWithVat()` will really be the price of the article including the vat.

**Remark**

With this definition, a developer may understand `s` even if `getPriceWithVat()` will return a value which will not be correct. He is only able to predict that *if there is no bug in the implementation of the imported references of `s`* (*i.e.* if their behavior corresponds to their role), then `getPriceWithVat()` will return the correct price including VAT. 

This is not in contradiction with the intuitive notion of code understanding: with the definition above, if a developer understands `s`, he will be able to detect if the real behavior of `s` is correct or not, and thus if there is a bug or not. This is probably what we intuitively mean when we say that a developer understands a code snippet: he is able to debug it.

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
 
By extension, the ***refactoring of a feature*** is the action to transform the set of code snippets implementing a feature `f` in a different set of code snippets implementing the same feature `f`. 

Same definition for the ***refactoring of a program***.


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
if (a > 0) { 
	return 1; 
} else {
	return 2;
}
console.log('Hello World !');
```
The last line is a dead code, so we can remove it without changing the behavior of the program.

```ts
// Code snippet s'
if (a > 0) {
  return 1;
} else {
  return 2;
}
```

The role of `s'` is the same as `s`, so the operation `r: s -> s'` is a refactoring. The second line of `s` was not empty, and any non-empty code snippet is strictly higher than 0. Thus, by removing the second line of `s`, we decreased its cognitive complexity. We have

`Cc(r(s)) < Cc(s)`

This example demonstrates that a refactoring may decrease the cognitive complexity of a code snippet. 

You will find here a study of some [simplification technics](simplification-technics.md).


***Work in progress...***
