# The understanding

The definition of the [cognitive complexity](cognitive-complexity.md) uses the word `understand`. We need to accurate what we mean when we use this term. In other words, we need to precise what are the attributes of what we call *"understanding"*, how they are correlated to the cognitive complexity, and how we could measure them in the real world.

At first, our goal is not to define what is *understanding* in all the situations where this word can be used, but only in the context of the *software understanding*. Our aim is to define the *understanding* relatively to a [code snippet](code-snippets.md), not in other situations.

## Table of contents

* [Role and behavior](#role-and-behavior)
* [Understanding of references](#understanding-of-references)
* [Persistence over time](#persistence-over-time)
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
> A developer `d` ***understands the role of a reference*** `r` if he is able to guess the predictions of the author of `r` about the [behavior](code-snippets-tmp.md#roles-and-descriptions) of `r`.

**Remark**

This definition doesn't mean that a developer understands a reference `r` when he is able to predict its behavior, but only if he is able to guess the *same predictions* than the author of `r`. Moreover, these predictions may be wrong (in this case, `d` introduced a bug).


> **Definition**
>
> A developer ***understands the declaration of a reference*** `r` if he understands its role without the help of its implementation.
>
> A developer ***understands the implementation of a reference*** `r` if he understands its role without the help of its declaration.


> **Definition**
> 
> A developer `d` ***understands a reference `r` in the context of a valid code snippet `s`*** if:
> * `r` is imported in `s`
> * `d` understands the role of `r`
> * `d` is able to predict the behavior of `r` when `r` is called by `s`
>
> A developer `d` ***understands a reference*** `r` if:
> * `d` is able to understand `r` in the context of any valid code snippet
> * `d` understands the implementation of `r`

> **Proposition**
>
> A developer understands the role of a reference `r` if he is able to predict if there is a bug in the implementation of `r`.

**Demonstration**

// TODO

[comment]: <> (> **Definition**)

[comment]: <> (>)

[comment]: <> (> The ***cognitive complexity of an imported reference*** `r` located in a given snippet `s` is the time needed by a mean developer to predict the behavior of the system when this reference will be called by a given process `p`.)

[comment]: <> (> )

[comment]: <> (> The ***cognitive complexity of an exported reference*** `r` located in a given snippet `s` is the time needed by a mean developer which will import this reference to predict the behavior of the system when this reference will be called by a given process `p`.)

[comment]: <> (> **Definition**)

[comment]: <> (>)

[comment]: <> (> The ***cognitive complexity of a reference*** `r` written by a developer `d` is the time needed by a mean developer `d'` to understand its role.)

[comment]: <> (>)

[comment]: <> (> The ***relative cognitive complexity of a reference*** `r` imported in a context-sensitive code snippet `s` is the time needed by a mean developer to predict its role on the context of `s`.)

## Persistence over time

When a program is finished, the specs are usually lost. The developers needed them to write the code, but when their work is finished, it is only the code which is persisting over time, not the specs, which were probably given orally, or written in an external software like JIRA.

So, when a new developer will need to fix bug or add new features, its only information is provided by the code. He doesn't know the original specs. Similarly, he has no information about the *role* of a code snippet, which is something which was *in the mind of the developer which wrote it*. Its only information is the *description* of this role, which was written by the previous developer.

The descriptions and the implementations are the only things persisting over time. They are the only available information to the new developer which wants to *understand* the code.


## Understanding of valid code snippets

> **Definition**
>
> A developer ***understands a context-sensitive valid code snippet*** `s` if :
> 1. he understands the role of each [reference](code-snippets-tmp.md#references) declared in `s`.
> 2. he understands the role of each reference imported in `s`, in the context of `s`.
> 3. if the behavior of the imported references of `s` corresponds to their roles, he is able to predict the behavior of each reference declared in `s`.

**Example**

Assume that a developer `d` wrote a code snippet `s` consisting in a function `getPriceWithVat` whose *role* is to return the prive including VAT of a given article.

```ts
// Code snippet s
function getPriceWithVat(article: Article): number {
	const price: number = article.getPrice();
	const vat: number = VAT_RATE * price;
	return price + vat;
}
```

A developer `d'` *understands* `s` if :

*1. Role of the references declared in `s`*

- he understands that the role of `getPriceWithVat()` is to return the prive including VAT of a given article.
    
*2. Role of the references imported in `s`*

- he understands that `Article` is a class whose role is to represent the different articles.
- he understands that `getPrice()` is a method of the class `Article` whose role is to return the pre-tax price of the article.
- he understands that `VAT_RATE` is a constant whose role is to provide the vat rate to use.
  
*3. Behavior of the references declared in `s`*

- he predicts that `getPriceWithVat()` is correctly implemented, *i.e.* that if he understood well the role of the references declared or imported in `s`, the behavior of `getPriceWithVat()` will really be to return the price including VAT of an article.


[comment]: <> (> **Definition**)

[comment]: <> (>)

[comment]: <> (> A developer ***understands a context-sensitive valid code snippet*** `s` if he is able to predict the behavior of each [reference]&#40;code-snippets-tmp.md#references&#41; declared in `s` or imported in `s`.)

[comment]: <> (* Example)

[comment]: <> (Assume that a developer `d` wrote a code snippet `s` consisting in a function `getPriceWithVat` whose *role* is to return the prive including VAT of a given article.)

[comment]: <> (```ts)

[comment]: <> (// Code snippet s)

[comment]: <> (function getPriceWithVat&#40;article: Article&#41;: number {)

[comment]: <> (	const price: number = article.getPrice&#40;&#41;;)

[comment]: <> (	const vat: number = VAT_RATE * price;)

[comment]: <> (	return price + vat;)

[comment]: <> (})

[comment]: <> (```)

[comment]: <> (A developer `d'` *understands* `s` if :)

> **Proposition**
> 
> A developer understands a bugged context-sensitive valid code snippet if and only if he is able to locate any bug which would be transmitted to him.

**Demonstration**

* Let `s` a context-sensitive valid code snippet having some bugs. Let `d` the author of `s`, and let `d'` a developer which understands `s`. Assume that `d'` is informed of the existence of a bug `b` on a reference `r` declared in `s`. That means that `d'` knows the state of the system causing a wrong behavior to `r`. Thus, `d'` knows two things: 
    * An initial state of the system, called *s<sub>0</sub>*
    * A final state of the system, called *s<sub>1</sub>*, which is different from the expected state.
  
  As `d'` understands `s`, he understands the role of each reference declared in `s` (1.). Thus, he knows the role of `r`.

// TODO : finish demonstration

**Remark**

With the definition above, a developer may understand `s` even if `getPriceWithVat()` will return a value which will not be correct. He is only able to predict that *if there is no bug in the implementation of the imported references of `s`* (*i.e.* if their behavior corresponds to their role), then `getPriceWithVat()` will return the correct price including VAT. 

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
