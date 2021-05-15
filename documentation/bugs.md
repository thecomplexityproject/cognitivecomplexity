# Bugs

If we are so interested in the concept of cognitive complexity, it's because of its correlation with the software maintainability. A software is easier to maintain if the bugs are easy to fix than if they are difficult to find and to resolve.

Bugs may be caused by the program or by the system itself (hardware, connections, etc.). When we will use the word *bug*, it will be supposed that the problem is caused by the program, not by the hardware or something else.

## Definition of a bug

> **Definition**
>
> A program has a ***bug*** when the [behavior of the system](systems.md) does not respect the [specs](code-snippets-tmp.md#features) asked by the [prime contractor](code-snippets-tmp.md#features).

**Remark**

Assuming that no one prime contractor will ask to develop a feature which will make crash the app, we will suppose that any program which may crash in a real execution has a bug.

**Example**

Assume that the prime contractor asked to display the price of some articles on a web page. Assume now that a lead developer, as intermediate contractor, asks a developer to code a function which will return the price of a given article : 

Here is his code snippet: 
```ts
// Code snippet s
function getPrice(article: Article): number {
	return article.price;
}
```

If it is absolutely sure that the parameter `article` will never be undefined, *and* that the property `price` corresponds to the value expected by the client, there is no bug. If the parameter `article` may be undefined, there is a bug, because the app will crash when `article` will be undefined.

**Remark**

This example clearly demonstrates that we can't say that a code snippet has a bug in absolute terms, without specifying the specs expected by the prime contractor. 

## Causes of bugs

The causes of bugs are multiple, and the "wrongdoer" may not be the developer... Let's try to clarify it :

### Misunderstanding

The main cause of bugs is probably a misunderstanding between two consecutive links of the [chain of responsibilities](code-snippets-tmp.md#features).

> **Definition**
> 
> A ***misunderstanding*** between two consecutive element of a chain of responsibilities happens when there is a difference between what thinks the superior element and what the inferior element thinks that his superior thinks.

**Example 1**

Assume that a client asks a developer to code a function which will return the price of a given article, in the aim to display its price on a web page. If it was clear in the mind of the client that the displayed price must be the pre-tax price, and if the developer thought that it should be the price including the VAT, there is a misunderstanding between the client and the developer.

If it was not explicitly specified that the price must be without VAT, *it is not a bug*, because the developer respected the specs explicitly given by the client. It is a lack of specs. In this case, the client is the wrongdoer. If it was explicitly specified, it is a bug, and the developer is the wrongdoer.

**Example 2**

Assume now that we add a link to the chain of responsibilities: a lead developer. If the client explicitly specified that the price must be without VAT, and if the lead developer didn't give this information to the developer, there will be a bug, but the wrondoer will be the lead developer.

### Wrong implementation

> **Definition**
>
> A program has a ***wrong implementation*** when there is no misunderstanding, and when the behavior of the system does not respect the specs of the different features asked by the prime contractor.

**Example**

In the example above, assume that the client wanted to display the pre-tax price, and there was no misunderstanding in the chain of responsibilities. If the displayed value is not the pre-tax price of the article, there is a wrong implementation. 

**Remark**

In case of wrong implementation, the wrongdoer may not be the developer. For example, an architect may ask developers to implement some functionalities. All the code snippets may respect the specs asked by the architect, but the combination of all these code snippets may not provide the behavior expected by the client. In this case, the wrongdoer is the architect.

### Wrong reuse

> **Definition**
> A ***reuse*** of a program, a feature or a code snippet, is its use in a context defined by different specs. 

**Example**

Assume that a client asked to develop a web page displaying the pre-tax of a some articles. Assume that there is no bug, and that the code snippet below returns the correct value :

```ts
// Code snippet s
function getPrice(article: Article): number {
	return article.price;
}
```

Now, assume that the client wants a second page displaying the pre-tax of other articles. If the implementation of this new feature uses `s`, it is a reuse of `s`.



> **Definition**
>
> A context-sensitive valid code snippet has a ***bug*** when its role is different from its behavior.

**Caution**

The [role](code-snippets-tmp.md#behaviors-roles-and-descriptions) of a code snippet `s` is a subjective notion, which is relative to the author of `s` (*The role of a context-sensitive valid code snippet `s` is the [behavior of the system](systems.md) expected by the author of `s` when another code snippet calls one of the exported references of `s`*).

Consequently, by definition, a *bug* is also a subjective notion relative to the author of `s`. A bug is not something which is absolute, independent of the context.

* *Example 1: bug caused by a misunderstanding*

Assume that a client ask a developer to create a function which will return the price of an object of type `Article`.


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
