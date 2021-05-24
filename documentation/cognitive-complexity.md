[<-](README.md)
# Cognitive Complexity

## Table of contents

* [Definitions](#definitions)
    * [Cognitive complexity](#--cognitive-complexity)
    * [Cognitive complexity metric](#--cognitive-complexity-metric)
    * [Relation between cognitive complexity and debugging](#--relation-between-cognitive-complexity-and-debugging)
    * [Minimal cognitive complexity](#--minimal-cognitive-complexity)
* [Refactoring](#refactoring)
    * [Definition of refactoring](#definition-of-refactoring)
    * [Simplifications](#simplifications)

[-> Top](#cognitive-complexity)
## Definitions

##### -> Cognitive complexity
> **Definition**
> 
> The ***cognitive complexity*** of a code snippet is the time required by a [mean developer](mean-developer.md) to [understand](understanding.md#--understanding-of-code-snippets) it.


##### -> Cognitive complexity metric
> **Definition**
>
> We call ***cognitive complexity metric*** the function which assigns to each code snippet its cognitive complexity. This metric is noted ***Cc***.
>
> If ***S*** is the set of code snippets and ***R<sup>+</sup>*** the set of the real positive numbers, we have
> ```ts
> Cc:  S   ->   R+
>     s   ->   cognitiveComplexity(s)
> ```


##### -> Relation between cognitive complexity and debugging
> **Proposition**
>
> The cognitive complexity of a code snippet `s` is equal to the time needed by a mean developer to predict if, for each reference `r` declared in `s`, `r` has a bug or not.

**Demonstration**

* The demonstration is trivial with the definition of the cognitive complexity [above](#--cognitive-complexity) and the definition of the [understanding of a code snippet](understanding.md#--understanding-of-code-snippets).


##### -> Minimal cognitive complexity
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

[-> Top](#cognitive-complexity)
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
