# Bugs

If we are so interested in the concept of cognitive complexity, it's because of its correlation with the software maintainability. A software is easier to maintain if the bugs are easy to fix than if they are difficult to find and to resolve.

## Definition of a bug

> **Definition**
>
> A context-sensitive valid code snippet has a ***bug*** when its role is different from its behavior.

**Caution**

The [role](code-snippets-tmp.md#behaviors-roles-and-descriptions) of a code snippet `s` is a subjective notion, which is relative to the author of `s` (*The role of a context-sensitive valid code snippet `s` is the [behavior of the system](systems.md) expected by the author of `s` when another code snippet calls one of the exported references of `s`*).

Consequently, by definition, a *bug* is also a subjective notion relative to the author of `s`. A bug is not something which is absolute, independent of the context.

* *Example 1: bug caused by a misunderstanding*

Assume that a client ask a developer to create a function which will return the price of an object of type `Article`.

```ts
// Code snippet s
function getPrice(article: Article): number {
	return article.price;
}
```

For the developer, there is no bug. However, if the client asked to return the price *including the VAT*, there is a bug.

* Example 2: bug caused by a reuse

Assume now that the developer fixed the first bug like this:

```ts
// Code snippet s
function getPriceWithVat(article: Article): number {
	return article.priceWithVat;
}
```

Now, assume that 6 months later, another developer reuse this method on a new feature, which must return the price 

```ts
// Code snippet t
function getPriceWithVat(articleName: string): number {
	const article: Article = getArticleInDatabase(articleName);
	return getPriceWithVat(article);
}
```


**Remark**

By convention, we will suppose that any non-valid code snippet has a bug.

> **Definition**
>
> A ***bug fix*** is an operation from **S** to **V** which transforms a code snippet `s` having some bug in a code snippet `s'` which has a behavior equal to the supposed behavior of `s`.

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

***Work in progress...***
