# The understanding

The definition of the [cognitive complexity](./cognitive-complexity.md) uses the word `understand`. We need to accurate what we mean when we use this term. In other words, we need to precise what are the attributes of what we call *"understanding"*, how they are correlated to the cognitive complexity, and how we could measure them in the real world.

At first, our goal is not to define what is *understanding* in all the situations where this word can be used, but only in the context of the *software understanding*. Our aim is to define the *understanding* relatively to a [code snippet](code-snippets.md), not in other situations.

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

## Roles and features

> **Definition**
>
> A ***role*** is a description of a possible modification of the [state of the system](code-snippets.md).
> 
> The ***role of a code snippet*** is a description of its possible impact on the state of the system.

The *role of a code snippet* `s` could be interpreted as the ***signified*** of `s`.

**Remark**

Multiple code snippets may have the same role.

> **Definition**
>
> A developer ***understands the role of a code snippet*** `s` if he is able to predict what will be the modifications to the [state of the system](code-snippets.md#systems) when some part of `s` will be executed by a given [process](code-snippets.md#systems) `p`.

With the previous example, this definition means that a developer understands that when the function `multiplyByTwo` will be called, the piece of code of the system which called this function with a parameter `a` will receive in return the double of `a`.

In which cases this definition could be interesting ? It seems to be too simple to have a real utility, but that's not so sure.

* Example

```ts
// Code snippet t

function multiplyBySix(a: number): number {
	const b: number = multiplyByTwo(a);
	return b * 3;
}
```

When a developer reads the code snippet `t`, he doesn't need to know *how* the function *multiplyByTwo* will really multiply `a` by 2. He only needs to understand what will be the value of `b` when the function `multiplyByTwo` will be called. In other words, he needs to understand the *role* of this function, not its *implementation*.

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

In conclusion, we just need to remember that the understanding of the role of the code is important in the aim to understand *other* code snippets (and debug them easier).

> **Definition**
> 
> A ***feature*** is a functionality provided by the [system](code-snippets.md) to the users.



## Implementation

> **Definition**
>
> An ***implementation*** of a feature is a set of code snippets of a given [program](code-snippets.md) which are mandatory to provide this feature to the user.
>
> By extension, we say that a code snippet implements a given role when the modification of the [state of the system](code-snippets.md) is described by this role.

**Trivial remarks**

* The set of the implementations of a given role is infinite. 
* The set of the implementations of a given feature is infinite.

> **Definition**
>
> A developer ***understands the implementation*** of a code snippet `s` if he is able to understand the role of each code snippet included in `s`.

Now, we are able to define exactly what the verb *understand* means in the definition of the [cognitive complexity](cognitive-complexity.md):

* Example

```ts
// Code snippet s
function f(a: number): number {
	return a * 2;
}
```

When the developer reads the first line, he can't understand its role. After reading the second and the third line, he will understand the role of these two lines, but also the role of the first one (the function itself). At the end, he will understand everything: the role of `s` and the role of each of its parts.

> **Definition**
> 
> A developer ***understands*** a code snippet if he understands its role and its implementation.

## Minimal cognitive complexity

> **Definition**
> 
> The ***minimal cognitive complexity*** of a role `r` is the lower limit of the cognitive complexities of the set of code snippets implementing `r`.



## Refactoring


> **Definition**
> The ***refactoring*** is the action to transform a code snippet `s` in a code snippet `t` which has the same role as `s`.
> 
> By extension, the refactoring of a feature is the action to transform a feature `f` in a feature `g` which provides the same functionalities to the users.
>


