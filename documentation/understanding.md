# The understanding

The definition of the [cognitive complexity](./cognitive-complexity.md) uses the word `understand`. We need to accurate what we mean when we use this term. In other words, we need to precise what are the attributes of what we call *"understanding"*, how they are correlated to the cognitive complexity, and how we could measure them in the real world.

At first, our goal is not to define what is *understanding* in all the situations where this word can be used, but only in the context of the *software understanding*. Our aim is to define the *understanding* relatively to a [code snippet](code-snippets.md), not in other situations.

## Table of contents

* [Where is the problem ?](#where-is-the-problem-)
* [Definition of *understanding*](#definition-of-understanding)
* [Minimal cognitive complexity](#minimal-cognitive-complexity)
* [Refactoring](#refactoring)
    * [Definition of refactoring](#definition-of-refactoring)
    * [Refactoring methods to decrease the cognitive complexity](#refactoring-methods-to-decrease-the-cognitive-complexity)    

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

## Definition of *understanding*

> **Definition**
>
> A developer ***understands the role of an external reference*** `r` located in a code snippet `s` if he is able to predict, when a process calls `r`, the same [behavior of the system](systems.md) than the developer which *wrote* the implementation of `r`.

> **Definition**
>
> The ***cognitive complexity of an external reference*** `r` located in a given snippet `s` is the time needed by a mean developer to predict the behavior of the system when this reference is called by a given process `p`.

> **Definition**
>
> A developer ***understands a code snippet*** `s` if he understands the role of each [external reference](code-snippets-tmp.md#roles) located in `s`, and if he is able to predict the [behavior of the system](systems.md#definitions) when `s` is executed by a given [process](systems.md#definitions) `p`, assuming that the supposed roles of the external references are correct.

**Remark**

This definition doesn't mean that a developer understands a code snippet when he is able to predict the behavior of the system when a process calls the code snippet, but that he is able to do the *same predictions* that the authors of the external references would do. 

* Example

```ts
// Code snippet s
function getBill(article: Article): number {
	const price: number = article.getPrice();
	const vat: number = VAT_RATE * price;
	return price + vat;
}
```

A developer *understands* `s` if he understands that:

- it is a function called `getBill` which takes an `Article` in parameter, and that its role is to return the bill of a given article.
- `getPrice()` is a method of the class `Article` which will return the price of the article.
- `VAT_RATE` is the vat rate to use
- the returned value is the price of the article including the vat

*AND* if the author of `Article`, `getPrice()` and `VAT_RATE` thought that:

- the role of `Article` is to represent an article
- the role of `getPrice()` is to return the price of an article without vat
- the role of `VAT_RATE` is to give the value of the vat rate.

What kind of errors could happen when a developer reads this code snippet ?

* There is a difference between the role thought by the author of the external references, and the role imagined by the reader (misunderstanding between the author and the reader, maybe because of a *low quality level of the description* of the references)
* The reader understands correctly the role of the external references as thought by their author, but these references have a behavior in contradiction with their supposed role (the *author* made an error)
* The reader understands correctly the role of the external references as thought by their author, these roles were correctly implemented, but the reader misunderstands the implementation of `getBill()` itself (the *reader* made an error)

With the previous example, this definition means that a developer understands that when the function `multiplyByTwo` will be called, the piece of code of the system which called this function with a parameter `a` will receive in return the double of `a`.

Remember that if we are so interested in the cognitive complexity, it's because of its correlation with the software maintainability. A software is easier to maintain if the bugs are easy to fix than if they are difficult to find and to resolve. 

Bugs are difficult to find if the code is difficult to understand, and the code will be difficult to understand if the *meaning* of some parts of the code are not clear. The code snippet `t` is simple and easy to debug because the role of the function `multiplyByTwo` is trivial. We don't need to read the code snippet `s` to understand `t`.

All of this simply means what every good developer already knows: the names of the variables, classes, functions or methods must be as clear as possible. It is a problem of *readability*, which will be studied in details later.

Now, assume that the name of the function of the code snippet `s` was not correctly defined and that we try to use it in another code snippet `t`:

```ts
// Code snippet s
function someFunction(a: number): number {
	// Do complex operations and return some number
}

// Code snippet t
function doComplexCalculations(a: number): number {
	const b: number = someFunction(a);
	// Do some long calculations using b
	return b;
}
```
The code snippet `t` is impossible to debug without reading `s`: the *role* of `s` is not understandable in `t`. 

So, if you want to debug `t`, you'll read the code of `s`, but in the aim to understand *what* `someFunction` is doing, not *how* `someFunction` runs. The most important for you is the *role* of `s`, not its `significant`. The *role* of `s` will become important for you if and only if the bug is inside `s`.

It is also the justification of the *documentation*: if `someFunction` is correctly documented, you'll not need to understand its implementation :

```ts
// Code snippet s

// Returns the circumference of a circle of radius a
function someFunction(a: number): number {
	// Do complex operations and return some number
}
```

The comments and the names of the identifiers are probably the most important parameters correlating the cognitive complexity with the understanding of the role of the code snippets, but are not the only ones. Moreover, we could discuss of the real efficiency of the documentation in some specific cases: do we really need documentation for very trivial cases, like for the function `multiplyByTwo` ? Or for the getters and the setters ? If not, in which cases should we add some documentation, and what should we write inside ? We could debate hours and hours about it, without having objective and indiscutable results: we would only have different expert opinions. We need scientific experiments, measures and statistics to be able to say one day: "yes, you should write documentation here, because it is proven that it will reduce the cognitive complexity".

In conclusion, we just need to remember that the understanding of the *role* of the code is important in the aim to understand *other* code snippets (and debug them easier).

> **Definition**
>
> A developer ***understands*** a valid code snippet `s` if he understands the role of each code snippet included in `s` (including `s` itself).

**Remark**

A code snippet containing more than one [string](code-snippets-tmp.md#code-snippets)

Now, we are able to define exactly what the verb *understand* means in the definition of the [cognitive complexity](cognitive-complexity.md):

* Example

```ts
// Code snippet s
function f(a: number): number {
	return a * 2;
}
```

When the developer reads the first line, he can't understand its role. After reading the second and the third line, he will understand the role of these two lines, but also the role of the first one (the function itself). At the end, he will understand everything: the role of `s` and the role of each of its parts.

**Remark**

This definition doesn't imply that the cognitive complexity of a code snippet is the sum of the duration needed to understand its role, and the duration needed to understand its implementation. In the example above, 

[-> Top](#the-understanding)
## Minimal cognitive complexity

> **Definition**
> 
> Let `s` a valid code snippet and `b` its behavior.
> The ***minimal cognitive complexity*** of `b` is the lower limit of the cognitive complexities of the set of code snippets having this behavior.


[-> Top](#the-understanding)
## Refactoring

### Definition of refactoring

> **Definition**
> 
> The ***refactoring*** is the action to transform a valid code snippet `s` in one or multiple valid code snippets *t<sub>1</sub>, ... t<sub>n</sub>* which collectively have the same behavior as `s`. The refactoring is an operation from **[V](code-snippets-tmp.md#valid-code-snippets)** to **V**<sup>n</sup>.
> 
> *r: (s ∈ V) -> (t<sub>1</sub>, ... t<sub>n</sub> ∈ V<sup>n</sup>)*
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

This example demonstrates that a refactoring may decrease the cognitive complexity of a code snippet. We can now try to find useful [simplification technics](simplifications.md).


