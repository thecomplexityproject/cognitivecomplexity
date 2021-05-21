# Simplifications technics

In the aim to increase software maintainability by decreasing cognitive complexity, the developers will use many refactoring technics. Some of them are efficient, but others are probably not. There is a high probability that sometimes, the refactoring operations are increasing the cognitive complexity instead of decrease it. Some technics are efficient in any cases, and others only in some specific situations.

The aim of this page is to study the impact of the different [refactoring technics](understanding.md#simplifications) on the value of the Cognitive Complexity.

## Table of contents

* [Remove the dead code](#remove-the-dead-code)
* [Clarify identifiers](#clarify-identifiers)
* [Add comments](#add-comments)
* [Typing](#typing)
* [Logic extraction](#logic-extraction)
* [Remove line-breaks](#remove-line-breaks)


## Remove the dead code

> **Proposition**
>
> The refactoring which consists of removing the dead code is a simplification.

> *Demonstration*
>
> Let `s` a context-sensitive valid code snippet.
> 1. The action consisting of remove the dead code of `s` is a refactoring because it doesn't change its behavior.
> 2. Any non-empty code snippet has a cognitive complexity strictly higher than 0.
> With 1. and 2., we can assert that the removing of the dead code is a simplification.


## Clarify identifiers

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

## Add comments

> **Conjecture**
>
> Let `r` a refactoring consisting of adding comments, and `s` a given context-sensitive valid code snippet.
> `r` may decrease or increase the cognitive complexity of `s`.

* Example 1 (decreasing cognitive complexity)

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


* Example 2 (increasing cognitive complexity)

```ts
// Code snippet s
function multiplyByTwo(a: number): number {
	return a * 2;
}
```

The code snippet `s` is very easy to understand. The only exported reference is the function `multiplyByTwo()`; its role is trivial, the developer does not need to read after the name of the function to guess its role. There is no imported reference, and the implementation of this function is trivial. Consequently, why the developer should read some comments to understand `s` ?

Assume that we refactor `s` by adding some comments :

```ts
// Code snippet r(s)

/**
 * This function will return the result of the multiplication by 2 of a given number
 * @param a: number // The number to multiply by 2
 */
function multiplyByTwo(a: number): number {
	return a * 2;
}
```

Is `r(s)` easier to understand than `s` ? Probably not. Thus, a refactoring consisting of adding comments to a given code snippet may increase its cognitive complexity.

## Typing

Some languages, like JavaScript, don't provide the ability to type the variables, or the functions. The language TypeScript is an overcoat layer of JavaScript, which was developed in the aim to fill this gap. The final goal of TypeScript is to limit the risk of bugs due to the lack of typing. Is a typed code snippet simpler to understand than if it was untyped ? Probably yes :

> **Conjecture**
>
> In non-trivial cases, a typed code snippet `s` has a cognitive complexity lower than the code snippet `r(s)`, where is the refactor operation which consisting of remove all the types of `s`.


**Example**

```ts
// Code snippet s
let a = f(1); 
```

```ts
// Code snippet t
let a: Article = f(1);
```

The first code snippet `s` is difficult to understand, because we don't know the *role* of `a`. It is an *exported reference* that we are not able to understand. 

In contrast, in the code snippet `t`, we intuitively understand that `a` is an object of the type `Article`. We understand its role, and we would easily understand later some code snippets like `a.price`, `a.name`, `a.description` or `a.brand`.

We conjecture that `Cc(t) < Cc(s)`.

**Remark**

We must specify what is a *non-trivial case*. For now, we can only give a list of simple cases where the cognitive complexity seems to be higher when the code is typed.

* Variable declarations with implicit Literal Type :

`Cc("let a: string = 'a';") > Cc("let a = 'a';")`

* Variable declarations with the keyword `new` :

`Cc("let a: Article = new Article();") > Cc("let a = new Article();")`


## Logic extraction

Huge functions, with hundreds of lines and complex operations, are usually regarded as non-readable and incomprehensible. It is probably true. However, is it *always* true ? If not, in which cases is it true ?

**Example of relevant refactoring**

We saw [here](understanding.md#minimal-cognitive-complexity) an example of relevant functions splitting :

```ts
// Code snippet s
export function getProfile(id: number): Profile {
  if(isClientId(id)) {
    // Do some long stuff returning the profile of the client corresponding to the given id
  } else {
    // Do some long stuff returning the profile of a company corresponding to the given id
  }
}
```

The refactored code snippet :

```ts
// Code snippet r(s)
export function getProfile(id: number): Profile {
  return isClientId(id) ? getClientProfile(id) : getCompanyProfile(id);
}

function getClientProfile(id: number): Profile {
  // Do some long stuff returning the profile of the client corresponding to the given id
}

function getCompanyProfile(id: number): Profile {
  // Do some long stuff returning the profile of a company corresponding to the given id
}
```

In this case, it seems to be relevant to split `getProfile()`, because we can divide it in two parts having a role which is easy to specify, and because each part has a high cognitive complexity. After the refactoring, a developer which reads `getProfile()` will understand easier its implementation, which is now reduced to only one line calling two internal references: `getClientProfile()` and `getCompanyProfile()`. 

Moreover, in the original code snippet `s`, it was not easy to understand the role of the code inside the `if`, and even more for the `else`, because we have no information of what kind of `Profile` we have when the parameter `id` is not a `client id`. After the refactoring, we know immediately that when a `profile` is not a profile of a client, it is a profile of a company.

The function splitting provide us the possibility to specify the role of a *part* of the function, which may help its understanding.

**Remark**

Another usual technic to specify the role of a part of a function is to add some comments *inside the function*, like this:

```ts
// Code snippet s
export function getProfile(id: number): Profile {
  if(isClientId(id)) {
    // Do some long stuff returning the profile of the client corresponding to the given id
  } else { // it is the id of a company
    // Do some long stuff returning the profile of a company corresponding to the given id
  }
}
```

The comment *"it is the id of a company"* located after the `else` probably helps to understand the function, and thus decreases its cognitive complexity. However, we think that the first technique is more efficient, but we are not able to prove it for now.

**Example of relevant refactoring**

```ts
// Code snippet s
export function multiply(a: number): number {
     if(a > 0) {
          return a * 2;
     } else {
          return a * 3;
     }
}
```

```ts
// Code snippet r(s)
export function multiply(a: number): number {
     if(a > 0) {
          return multiplyByTwo(a);
     } else {
          return multiplyByThree(a);
     }
}

function multiplyByTwo(a: number): number {
     return a * 2;
}

function multiplyByThree(a: number): number {
     return a * 3;
}
```

In this case, it seems that the extraction of the logic *multiply by two* and *multiply by three* don't simplify `s`; rather, it seems that its cognitive complexity increased.

> **Definition**
> 
> The ***logic extraction*** is a refactoring technique consisting of extracting some part of a given code snippet `s` in a separate code snippet `s'` which will be called by `s`.

> **Conjecture**
> 
> The efficiency of the *logic extraction* technic is positively correlated with the cognitive complexity of the parts to extract. In other words, it is more relevant to extract a complex code snippet than a simpler one. 


## Remove line-breaks


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

It is usually recommended implementing this algorithm by using the form of `s` instead of the form of `r(s)`, for questions of readability. It is probably true that the initial form of `s` is more easy to read, and thus easier to understand. We can conjecture that `Cc(s) < Cc(r(s))`, thus `r` is probably not a simplification.

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
