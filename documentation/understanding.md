[<-](README.md)
# The understanding

The definition of the [cognitive complexity](cognitive-complexity.md) uses the word `understand`. We need to accurate what we mean when we use this term. In other words, we need to precise what are the attributes of what we call *"understanding"*, how they are correlated to the cognitive complexity, and how we could measure them in the real world.

At first, our goal is not to define what is *understanding* in all the situations where this word can be used, but only in the context of the *software understanding*. Our aim is to define the *understanding* relatively to a [code snippet](code-snippets.md), not in other situations.

## Table of contents

* [Introduction](#introduction)
* [Behavior](#behavior)
  * [Behavior prediction and understanding](#--behavior-prediction-and-understanding)
* [Role](#role)
  * [Role understanding of declared or imported references](#--role-understanding-of-declared-or-imported-references)
  * [Description understanding, implementation understanding](#--description-understanding-implementation-understanding)
  * [Reference understanding](#--reference-understanding)
* [Code snippets](#code-snippets)
  * [Understanding of code snippets](#--understanding-of-code-snippets)

[-> Top](#the-understanding)
## Introduction

Let's start with a simple example. 

```ts
// Code snippet s

function multiplyByTwo(a: number): number {
	return a * 2;
}
```

To define the word *understand* in the definition of the cognitive complexity, we could simply say: *a developer understands the function `multiplyByTwo()` if he is able to predict that the value returned by this function will be equal to the value of the parameter `a` multiplied by two*. In other words, we could say something like *"a developer understands `multiplyByTwo()` if he understands its implementation"*. Unfortunately, this is not enough to describe what we intuitively mean by *"understand"*. Let's look at the example below.

```ts
// Code snippet t

function multiplyByTwo(a: number): number {
  return a * 3;
}
```

If the developer understands the implementation, *i.e.* that this method will return a number multiplied by 3, but don't understand that there is a contradiction with the *name* of the function, should we say that he really understood this code snippet ? Surely not. A developer understands a function if he is able to predict its *expected behavior* and its *real behavior*.

The name of the function `multiplyByTwo()` clearly indicate that its *role* is to return a number multiplied by two. Its *implementation* is correct, because the *behavior of the system* will be as expected, *i.e.* will return the number multiplied by 2.

A developer really understands this function if he is able to understand its *role*, and if he is able to predict that its *implementation* is correct.  

[-> Top](#the-understanding)
## Behavior

##### -> Behavior prediction and understanding
> **Definition**
>
> A developer `d` is able to ***predict the behavior of a reference*** `r` if, for each [deterministic stub](code-snippets-tmp.md#--deterministic-stub) `s` of `r`, he is able to predict the state of the system after the execution of `s`. In this case, we say that `d` ***understands the behavior*** of `r`.

**Remark**

* The stub `s` must be deterministic. Consequently, if `r` uses a non-deterministic external reference `r'`, `r'` must be mocked.


[-> Top](#the-understanding)
## Role

##### -> Role understanding of declared or imported references
> **Definition**
>
> A developer `d` ***understands the role of a reference `r` declared in a code snippet `s`*** if he is able to guess the behavior of `r` predicted by its author when `r` is used by any code snippet.
>
> A developer `d` ***understands the role of a reference `r` imported in a code snippet `s`*** if he is able to guess the behavior of `r` predicted by its author when `r` is used by `s`.

**Remark**

* This definition doesn't mean that a developer understands the role a reference `r` when he is able to predict its behavior, but only if he is able to guess the *predictions of its author*. Moreover, these predictions may be wrong. In this case, the author of `r` introduced a bug.

##### -> Description understanding, implementation understanding
> **Definition**
>
> A developer ***understands the description of a reference*** `r` if he understands its role without the help of its implementation.
>
> A developer ***understands the implementation of a reference*** `r` if he understands its role without the help of its description.


##### -> Reference understanding
> **Definition**
>
> A developer `d` ***understands a reference `r` declared in a code snippet `s`*** if he guesses its role, and is able to predict its behavior.



> **Proposition**
>
> A developer understands a reference `r` declared in a code snippet `s` if and only if he is able to predict if `r` has a bug.

**Demonstration**

* The demonstration is trivial with the definition of a [bug of a reference](bugs.md#--bug-of-a-reference).

**Remark**

When a program is finished, the specs are usually lost. The developers needed them to write the code, but when their work is finished, it is only the code which is persisting over time, not the specs, which were probably given orally, or written in an external software like JIRA.

So, when a new developer will need to fix bug or add new features, its only information is provided by the code. He doesn't know the original specs. Similarly, he has no information about the *role* of a code snippet, which is something which was *in the mind of the developer which wrote it*. Its only information is the *description* of this role, which was written by the previous developer.

The descriptions and the implementations are the only things persisting over time. They are the only available information to the new developer which wants to *understand* the code.


[-> Top](#the-understanding)
## Code snippets

##### -> Understanding of code snippets
> **Definition**
>
> A developer ***understands a code snippet*** `s` if he understands each reference declared in `s`.

**Remark**

* In other words, a developer understands a code snippet `s` if, for each reference `r` declared in `s`, `r` has a behavior in contradiction with its role.


> **Proposition**
> 
> A developer ***understands a code snippet*** `s` if and only if he is able to predict, for each reference `r` declared in `s`, if `r` has a bug or not.


**Demonstration**

* The demonstration is trivial with the definition of a [bug of a code snippet](bugs.md#--bug-of-a-code-snippet).

[comment]: <> (> **Definition**)

[comment]: <> (>)

[comment]: <> (> A developer ***understands a code snippet*** `s` if :)

[comment]: <> (> 1. he understands the role of each [reference]&#40;code-snippets-tmp.md#references&#41; declared in `s`.)

[comment]: <> (> 2. he understands the role of each reference imported in `s`, in the context of `s`.)

[comment]: <> (> 3. assuming that the imported references of `s` have no bugs, he is able to predict the behavior of each reference declared in `s`.)

**Example**

Assume that a developer `d` wrote a code snippet `s` consisting in a function `getPriceWithVat` whose *role* is to return the price including VAT of a given article.

```ts
// Code snippet s
function getPriceWithVat(article: Article): number {
	const price: number = article.getPrice();
	const vat: number = VAT_RATE * price;
	return price + vat;
}
```

A developer `d'` *understood* `s` if :

*1. Role of getPriceWithVat()*

- he understood that the role of `getPriceWithVat()` is to return the prive including VAT of a given article.
    
*2. Behavior of getPriceWithVat()*

- he verified if the behavior of `getPriceWithVat()` corresponds to its role.
  
If one of the references imported in `s` has a bug, he will detect it.

**Remark**

* With these elements, we can now assert the equivalence between the cognitive complexity and the time needed to find the references having bugs (see [here](cognitive-complexity.md#relation-between-cognitive-complexity-and-debugging))



***Work in progress...***
