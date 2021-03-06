[<-](README.md)
# Code snippets

In the [cognitive complexity's definition](cognitive-complexity.md), the concept which is the most well-defined seems to be the notion of *code snippet*. That's probably true, but that doesn't mean that we can neglect to define it accurately. To be able to obtain scientific results, we need at first define precisely each word that we use. What is a *code snippet* ? A *valid code snippet* ? A *program* ? A *system* ? The *state of a system* ? All of these notions are defined more or less accurately in many scientific articles, and their definitions are more or less consensual.

In this project, we will specify our own definitions of simple or complex notions. That doesn't mean that we think that they will be better than the others, but simply that everyone should know accurately what *we* talk about when we use one of these definitions.

## Table of contents

* [Programming language](#programming-language)
  * [Alphabet, character](#--alphabet-character)
  * [Formal grammar](#--formal-grammar)
  * [Formal language](#--formal-language)
  * [Syntax](#--syntax)
  * [Programming language](#--programming-language)
  * [String](#--strings)
* [The set of code snippets](#the-set-of-code-snippets)
  * [Code snippet (large definition)](#--code-snippet-large-definition)
  * [Code snippet (close definition), context-sensitive valid code snippet](#--code-snippet-strict-definition-context-sensitive-valid-code-snippet)
  * [Context-free code snippet](#--context-free-code-snippet)
  * [Validatable code snippet](#--validatable-code-snippet)
  * [File](#--file)
  * [Module](#--module)
* [Implementation and behavior](#implementation-and-behaviors)
  * [Implementation](#--implementation)
  * [Behavior](#--behavior)
* [References](#references)
  * [Reference, identifier](#--reference-identifier)
  * [Description, declaration and implementation of a reference](#--description-declaration-and-implementation-of-a-reference)
  * [Exported and imported references](#--exported-and-imported-references)
  * [Exposed and hidden references](#--exposed-and-hidden-references)
  * [Behavior of a reference](#--behavior-of-a-reference)
* [Roles and descriptions](#roles-and-descriptions)
  * [Role of references](#--role-of-references)
  * [Quality level of descriptions](#--quality-level-of-descriptions)
* [Unit tests](#unit-tests)
  * [Stub](#--stub)
  * [Mock](#--mock)
  * [Deterministic stub](#--deterministic-stub)
  * [Deterministic reference](#--deterministic-reference)
  * [Unit test](#--unit-test)
* [Related definitions](#related-definitions)
  * [Separator](#--separator)
  * [Line of code](#--line-of-code)
* [Operations on code snippets](#operations-on-code-snippets)
  * [Addition](#--addition)
  * [Propositions and conjectures](#propositions-and-conjectures)


## Programming language

In theoretical computer science, we usually start by defining what is a computer language. In our case, it is not enough general, because our goal is to measure the time required for a developer to understand a code snippet, including code snippets having syntactic error, *i.e.* which are not respecting the rules of any language. We may want to measure the time that he will need to find a syntax error. That's why we will need, in the chapters below, to define different kinds of code snippets: *context-sensitive code snippets*, *context-free code snippets* and *non-valid code snippets*.

What is the doing a developer which wants to understand a program ? At first, he will open some files, read them, and try to understand them. Caution: each file is a document containing a text which may have different parts written in different languages. For example, a file may include some `html`, `javascript` and `php` code. That's why, when we'll need to define what is a bug and how to measure the debugging time, we will need a concept larger than a *programming language*. 

In fact, the reality is simple: when a developer opens a file, we only know he that he has a *text* to read, may be written in multiple languages. 


##### -> Alphabet, character
> **Definition**
> An ***alphabet*** is a set of symbols, letters, or tokens different from each other. The elements of this set are called the ***characters*** of the alphabet.

##### -> Strings
> **Definition**
>
> A ***string*** is a finite set of ordered individual elements of a given alphabet.

##### -> Formal grammar
> **Definition**
>
> A ***formal grammar*** is defined as a set of production rules for strings.


**Remark**
A grammar does not describe the meaning of the strings or what can be done with them in whatever context???only their form.

##### -> Syntax
> **Definition**
>
> A ***syntax*** is a set of rules of a formal grammar which defines the combinations of strings that are considered to be correctly structured statements or expressions.

##### -> Formal language
> **Definition**
>
> A ***formal language*** is a couple `(A, S)` where `A` is an alphabet and `S` a syntax relative to the strings formed with the elements of the alphabet `A`. 

**Remark**

There is a usual debate about the belonging of the markup languages -like HTML- in the set of the formal languages. We will not enter this debate, but as the markup files must be red and understood by developers, they are relevant for the cognitive complexity theory. Thus, we will include them in this set.

##### -> Programming language
> **Definition**
>
> A ***programming language*** is a formal language comprising a set of machine-readable instructions that produce various kinds of output.


[-> Top](#code-snippets)
## The set of code snippets

Now, we can define what is a *code snippet*:

##### -> Code snippet (large definition)
> **Definition**
>
> A ***code snippet*** is a couple (s, L) where `s` is a [text](#programming-language), `L` a [programming language](#programming-language).
> 
> A code snippet may be valid or not. It even may contains characters which are not included in the alphabet of `L`. Thereafter, when we will use the idiom *code snippet*, it will be supposed to be a *[context-sensitive code snippet](#--code-snippet-strict-definition-context-sensitive-valid-code-snippet)*

**Remarks**

* Thereafter, by abuse of language, we will simply note `s` a code snippet `(s, L)`. It will be implicit that a code snippet refers to some computer language `L` and to the program of a system containing `s`. Furthermore, a code snippet is supposed to be written in a single file.
* By convention, if `s` is an empty string, the couple `(s, L)` is also considered as a code snippet, and noted `''`.

**Example**

```ts
// Code snippet s
ab!z"{-a] =(r|???x
```
With the definition above, the couple (`s`, `TypeScript`) is a code snippet, even if it's not a valid TypeScript code.

Why do we need to have a so large definition of a *code snippet* ? Because we want to know what time will need a developer to understand some code, valid or not. When he will try to debug a TypeScript file, a developer can find a character which is not admitted by this language (and which will cause a syntax error).


##### -> Code snippet (strict definition), context-sensitive valid code snippet
> **Definition**
>
> A ***context-sensitive valid code snippet*** is a code snippet `(s, L)` where `s` respects the [context-sensitive grammar](https://en.wikipedia.org/wiki/Context-sensitive_grammar) of `L`. The set of the context-sensitive valid code snippets of a given language `L` is noted **V**<sup>+</sup>. Thereafter, when the idiom *code snippet* will be used without other precisions, it is always assumed that we talk about a *context-sensitive valid code snippet*.

##### -> Context-free code snippet
> **Definition**
>
> A ***context-free valid code snippet*** is a code snippet `(s, L)` where `s` respects the [context-free grammar](https://en.wikipedia.org/wiki/Context-free_grammar) of `L`. The set of the valid code snippets of a given language `L` is noted **V**.

##### -> Validatable code snippet
> **Definition**
>
> A ***validatable code snippet*** is a code snippet `(s, L)` which can be concatenated with another code snippet to give a context-sensitive valid code snippet. The set of the validatable code snippets of a given language `L` is noted **V**<sup>-</sup>.

**Remarks**

* A *context-sensitive valid code snippet* is a context-free valid code snippet.
* A *context-free valid code snippet* is a validatable code snippet.
* We will frequently call ***valid code snippet*** a *context-free valid code snippet*
 
**Example 1**

```ts
// Code snippet s
if (a > 0) {
  a = a + 1;
}
```
`s` is a *valid code snippet*, but not a *context-sensitive valid code snippet*, because `a` is not defined in `s`.

* Example 2

```ts
// Code snippet s
if (a > 0) {
```
`s` is not a *valid code snippet*, but is a *validatable code snippet*, because the concatenation of `s` with the code snippet `t` below is a valid code snippet.

```ts
// Code snippet  t
  a = a + 1;
}
```

**Remark**

The concatenation of the two code snippets must not have a letter on the both sides of the merge, like `va` + `r a = 2;`.

> **Proposition**
>
> Each subset of a valid code snippet is a validatable code snippet

This result ensues directly from the definitions of valid and validatable code snippets.

##### -> File
> **Definition**
>
> A ***file*** is a quadruplet (p, n, t, L) where `p` is a string which represents its path, `n` is a string which represents its name, `t` its content (*i.e.* the *text* of the file), and `L` is a given programming language.

**Remark**

Of course, in the real world, a file can't be defined with only these 4 elements, but for our purpose, we only need them.

##### -> Module
> **Definition**
>
> Let (p, n, t, L) a given file. The code snippet (t, L) is called a ***module***.

[-> Top](#code-snippets)
## Implementation and behaviors

##### -> Implementation
> **Definition**
>
> An ***implementation*** of a feature *-or a task-* is a set of code snippets which are providing a [behavior of the system](systems.md#--behavior-of-the-system) corresponding to the specs of the feature *-or the task-*.

##### -> Behavior
> **Definition**
>
> The ***behavior*** of a code snippet `s` is the [behavior of the system](systems.md#--behavior-of-the-system) when an external process calls one of the exported references of `s`, or executes the module where `s` is located. We say that `s` is an ***implementation*** of its behavior.

[-> Top](#code-snippets)
## References

##### -> Reference, Identifier
> **Definition**
>
> An ***identifier*** is a name chosen by a developer which represents a given data of the program: variables, constants, objects, functions, classes, properties, methods, interfaces, enums, types, etc.
> 
> The couple made up of an identifier and its value is called a ***reference***.


##### -> Description, declaration and implementation of a reference
> **Definition**
>
> The ***description of a reference*** `r` is the set of elements specifying its role. The description of `r` includes its name, its type, and its comments if they exist. 
> 
> The ***declaration of a reference*** `r` is the code snippet corresponding to its description.
>
> The ***implementation of a reference*** is the code snippet specifying its initial value or definition.


**Example**

```ts
// Code snippet s

/**
 * Returns the price of a given article
 * @param article
 */
function getPrice(article: Article): number {
	return article.price;
}
```

The *description* of the reference `getPrice` is the set of elements defined by its name, its signature and its comments.

Its *declaration* is the code snippet below:

```ts
/**
 * Returns the price of a given article
 * @param article
 */
function getPrice(article: Article): number {
	
}
```

Its *implementation* is:

```ts
	return article.price;
```

##### -> Reference of a code snippet
> **Definition**
>
> A ***reference of a code snippet*** `s` is a reference declared in `s`.

##### -> Exported and imported references
> **Definition**
>
> An ***exported reference*** is a reference declared in a code snippet `s` which is accessible outside of `s`.
> 
> An ***imported reference*** located in a code snippet `s` is a reference declared outside of `s`.

**Examples**
  
Assuming that each file may be called by some other part of the program, a [module](#--module) may be considered as an exported reference. 

##### -> Exposed and hidden references
> **Definition**
>
> Let `S` a set of code snippets.
>
> An ***exposed reference*** is an exported reference which is accessible from outside `S`.
>
> A ***hidden reference*** is an exported reference which is not accessible from outside `S`.

**Example**

* A library exposes some classes, functions or methods which are accessible from the rest of the world. In contrast, this library has certainly some classes, functions or methods which are exported from some code snippets, but which are accessible o,ly by the other code snippets of the application, not by the rest of the world.

**Remarks**

* A *public reference* is an exported reference, but may be not an exposed reference. For example, in TypeScript `node_modules`, the exposed references are usually declared in special declaration files, with the extension `.d.ts`. These files expose only the methods which should be called by the user of the `node_module`. The other public references are hidden.
* A module may be considered itself as an exported reference.

##### -> Behavior of a reference
> **Definition**
>
> The ***behavior of a reference*** `r` is the behavior of the system due to the usage of `r` during the execution of a given process.

**Remarks**

* If `r` is a variable, its behavior is defined by the variations of its value, and by the impact of the usage of `r` on the state of the system.
* If `r` is a function or a method, its behavior is defined by the variations of the state of the system when `r` is called, including its side effects.
* If `r` is a class, an interface, an enum or a type, its behavior is defined by the behavior of all the variables which are instantiated with the help of `r`.

[-> Top](#code-snippets)
## Roles and descriptions

When a task is transmitted to a developer, he will write some code snippets, in the aim to provide the expected behavior of the system, in the conditions given by the specs. For that, he will code some references, which will be exposed to the rest of the application, or to the rest of the world in the case of a public library. Each of these external references has a specific *role* to play in the aim to provide the expected behavior of the system in the context specified by the task.

##### -> Role of references
> **Definition**
>
> The ***role of a reference `r`*** is the behavior of `r` expected by its author when `r` is used by any code snippet.
>
> The ***role of a reference `r` in the context of a code snippet `s`*** is the behavior of `r` expected by its author when `r` is used by `s`.

**Remark**

* The role of a reference is a subjective notion. It is something which is in the mind of the author of the code snippet.
* The role of a reference `r` in the context of a code snippet `s` is the behavior of `r` expected by the author of `r` is he had written `s`.

**Example**

Here is the code snippet written by a first developer `d`:

```ts
// Code snippet s

/**
 * Returns the price of an article
 * @param article
 */
function getPrice(article: Article): number {
	return article.price;
}
```

In the mind of `d`, it is clear that the parameter `article` will never be undefined, because he knows that the program will never send to `getPrice()` an undefined value. For him, the *role* of the reference `getPrice` is to return the price of a non-undefined article.

Now, assume that 6 months later, a new developer `d'` must develop a new feature which needs to display the price of some article. For that, he will read the description of the function `getPrice` and will reuse it, thinking that its role is to return the price of the parameter `article` if this parameter is defined, and will return `undefined` if not. 

```ts
// Code snippet t

function logArticlePrice(articleId: number): number {
	const article: Article = getArticleFromDataBase(articleId);
	console.log(getPrice(article));
}
```

`d'` introduced a new bug, because the function `getPrice()` will crash when the value returned from the database will be undefined. This bug is a result of the misunderstanding between `d` and `d'`; the role of `getPrice` is not the same for `d` and `d'`.

The wrongdoer is `d'`, because he introduced the new bug: he should have done a unit test checking the case *"undefined"*. However, he introduced this bug because `d` used a bad coding practice: a function which may be imported y another module should never crash. `d'` introduced a *maintainability loophole*. It is a good example of *propagation of cognitive complexity*: if `d` had clarified the description of `getPrice`, `d'` had understood easier that he may introduce a bug. The bad practice of `d` increased the cognitive complexity of `getPrice` *and*, indirectly, the cognitive complexity of `getArticlePrice`.   

##### -> Quality level of descriptions
> **Definition**
>
> The ***quality level of a description*** of an exported reference `r` is said to be:
> * ***high*** if a mean developer is able to understand the role of `r` with only the name of `r` (and its signature for functions)
> * ***medium*** if a mean developer is able to understand the role of `r` with the name of `r`, its signature and its comments
> * ***low*** if a mean developer is able to understand the role of `r` with the name of `r`, its signature, its comments and its implementation


[<- Top](#code-snippets)
## Unit tests

##### -> Stub
> **Definition**
>
> A ***stub*** of a declared reference `r` is a code snippet which is written in the aim to simulate the behavior of `r` during the execution of a given process using `r` with some initial state of the system.

##### -> Deterministic stub
> **Definition**
>
> A stub `s` is ***deterministic*** if it is possible to predict the exact values of the data defining the state of the system after the execution of `s`.

**Remarks**

* In the definition above, the process executing the stub `s` is supposed to have a limited duration.
* Stubs are frequently confused with the *mocks*, which are defined below:

##### -> Mock
> **Definition**
>
> A ***mock*** is an object written in the aim to simulate the behavior of a given reference during the execution of a given stub.

**Remark**

* A mock is an *object*, which may have a value. A stub is a *code snippet*, which may use mocks.

##### -> Deterministic reference
> **Definition**
>
> A reference `r` is ***deterministic*** if each stub `s` of `r`is deterministic.

> **Proposition**
>
> For each reference `r`, it exists a deterministic stub of `r`.

**Demonstration**

* If `r` is deterministic, the result is trivial.
* If `r` is non-deterministic, it exists a non-deterministic stub `s` of `r`. Let `N` the set of non-deterministic external references of `s`. Each element of `N` may be replaced by a mock value, which is, by definition, deterministic. Let `s'` the sub obtained by a refactor of `s` consisting in replacing all the non-deterministic references of `s` by mocked values. `s'` is a deterministic stub of `r`.

##### -> Unit test
> **Definition**
>
> A ***unit test*** of a reference `r` is a code snippet written by the author of `r` in the aim to check if the behavior of `r` corresponds to its role when `r` is called by a given stub.
> 
> In other words, a unit test of a reference `r` is a code snippet written by the author of `r` in the aim to check if `r` has a bug.

**Remarks**

* A unit test checks if `r` have the behavior expected by its author, for the initial values which are simulated by some mocks.
* Thereafter, we will suppose that if the author of `r` wrote some unit tests, he verified if the behavior of `r` checked by the unit tests really corresponds to the role he gave to `r`.

> **Proposition**
>
> Let `r` a reference implemented by an author `a`. Let `t` a unit test relative to `r`, written by `a`. Let `d` a developer which is reading `r`.
>
> If `d` is not able to predict the behavior of `r` specified by `t`, `d` didn't understand the role of `r`.

**Demonstration**

* Assume that `d'` is not able to predict the behavior of `r` specified by `t`. That means that it exists a unit test `t`implemented with a stub which cause a behavior of `r` which is different from the behavior expected by `d'`. As we supposed that the developer `d` verified if the behavior of `r` checked by `t` is corresponding to the role he gave to `r`, we are sure that `d` made a prediction different from the prediction of `d'`. Consequently, by definition, `d'` didn't understand the role of `r`.

**Example**

// TODO

**Remark**

* The assertion *"a developer `d'` understands the role of a reference `r` if he is able to predict the behavior or `r` for each unit test written by the author of `r`"* is not true. `d'` may understand the unit tests actually written by the author of `r`, but may not understand future unit tests written by the author of `r`. If `d'` is able to predict the same behavior as written in a set of unit tests, he is only able to *partially* understand the role of `r`.

> **Proposition**
>
> Let `r` a reference implemented by a given developer `d`. Let `d'` another developer which is reading `r`.
>
> `d'` understands the role of `r` if and only if he would be able to predict the behavior of `r` specified by all the unit tests of `r` that `d` could write.

**Demonstration**

* Assume that `d'` does not understand the role of `r`. Thus, it exists a behavior of `r` which should be predicted by `d`, but not by `d'`. Consequently, `d` should write a unit test `t` corresponding to this behavior, and `d'` would not be able to predict the same behavior as written in `t`.
* Conversely, assume that `d'` is not able to predict the behavior of `r` specified by all the unit tests of `r` that `d` could write. That means that it exists a unit test `t` of `r` that `d` could write, which make predictions for a given stub which would the same as the predictions that `d'` would do. With the result of the proposition above, we can conclude that `d'` didn't understand the role of `r`.

[-> Top](#code-snippets)
## Related definitions


##### -> Separator
> **Definition**
>
> A ***separator*** is an invisible character. The characters which are not separators are called the ***visible characters***.

For example, whitespaces, tabulations and line breaks are separators.

**Remark**

The separators are usually not included in the formal language itself.

> **Proposition**
>
> The cognitive complexity of a separator may be null or non-null.

**Demonstration**

* *May be null:*

In Javascript, a whitespace at the end of a line of code is not visible and has no effect on the behavior due to the code snippet. Consequently, the developer will not need it to understand the code snippet. Thus, the cognitive complexity of this whitespace is equal to 0.

* *May be non-null:*

The tabulations are visually not distinguishable with a set of whitespaces (usually 2 or 4), but may be interpreted differently by a compiler or a browser, for example. Consequently, a developer may need some time to find a bug relative to a confusion between tabulations and whitespaces. In other words, he will need some time to understand the code snippet, which means that the cognitive complexity of whitespaces and tabulations may be strictly higher than zero.



Assuming that every computer language integrates the concept of "line break", we can give the following definition :

##### -> Line of code
> **Definition**
>
> The subset of a code snippet defined by the ordered characters between two consecutive line breaks is called a ***line of code***. If the code snippet has no line break, it has only one line of code which is the code snippet itself.

By definition, each line of code of a valid code snippet is a validatable code snippet.



[-> Top](#code-snippets)
## Operations on code snippets

##### -> Addition
> **Definition**
>
> We note **S<sub>L</sub>** the set of the *code snippets* (large definition, including non-valid code snippets) of a given formal language `L`, with the concatenation operation noted `+`.
>
> We note **V<sub>L</sub>**<sup>-</sup> the set of the [validatable code snippets](#--validatable-code-snippet) of a given formal language `L`, with the concatenation operation noted `+`.
>
> We note **V<sub>L</sub>** the set of the  of a given formal language `L`, with the concatenation operation noted `+`.
>
> We note **V<sub>L</sub>**<sup>+</sup> the set of the [code snippets](#--code-snippet-strict-definition-context-sensitive-valid-code-snippet) (strict definition, *i.e.* context-sensitive code snippets) of a given formal language `L`, with the concatenation operation noted `+`.

**Remark**

* By definition, we have **V<sub>L</sub>**<sup>+</sup> ??? **V<sub>L</sub>** ??? **V<sub>L</sub>**<sup>-</sup> ??? **S<sub>L</sub>**

**Notation**

For the sake of simplification, when the specification of the language is not needed, we will simply note **S**, **V**<sup>-</sup>, **V** and **V**<sup>+</sup> the sets of code snippets, validatable code snippets, context-free code snippets and context-sensitive code snippets of an implicit programming language **L**. 

**Remark**

The concatenation of two code snippets is a code snippet, so the operation `+` is an internal operation of **S**.
```
+ : (S x S)              ->    S
    'Hello' + ' world'   =     'Hello world'
```

> **Proposition**
>
> The operation `+` is an internal operation of **S**. In other words, if `s` and `t` are two code snippets, then `s + t` is a code snippet.

This result is trivial: the concatenation of two texts is a text.  


> **Proposition**
>
> The operation `+` is not an internal operation of **V**<sup>-</sup>, **V** or **V**<sup>+</sup>.
>
**Demonstration**

In TypeScript, assume that we have the valid code snippets `s` and `t` below :

```ts
// Code snippet s
let a = 2;

// Code snippet t
let a = 3;
```

The code snippet `s + t` is not valid, because the variable `a` is declared two times :
```ts
// Code snippet s + t
let a = 2;
let a = 3;
```

**Remark**

By contrast, the sum of a valid code snippet with a non-context-sensitive valid code snippet may be a valid code snippet.

*Example in TypeScript*

```ts
// Code snippet "s"
let a: number;

// Code snippet "t"
if (a > 0) { a = a + 1; }
```
`s` is valid and `t` is not context-sensitive valid, but `s + t` is context-sensitive valid :

```ts
// Code snippet "s + t"
let a: number;
if (a > 0) { a = a + 1; }
```


##### Propositions and conjectures


> **Conjecture**
>
> The cognitive complexity of the sum of two [code snippets](#--code-snippet-strict-definition-context-sensitive-valid-code-snippet) is strictly higher than the sum of the cognitive complexity of each of them.
<pre><code>C<sub>c</sub>(s + t) > C<sub>c</sub>(s) + C<sub>c</sub>(t)</code></pre>

The main reason of this result is that when the developer reads the second snippet, he must remember what happened in the first one, so the time that he needs to understand it is strictly higher than the time that he would need if this code snippet was alone.

* Example

```ts
// Code snippet s
if (a === 0) {
	return;
}

// Code snippet t
if (a < 5) {
	return 1 / a;
}

// Code snippet s + t
if (a === 0) {
	return;
}
if (a < 5) {
	return 1 / a;
}
```
In the example above, when you read the code snippet `s + t`, the cognitive complexity of the three first lines is the same as the complexity of `s`, because you have exactly the same information to understand. At the opposite, the three last lines will take more time to understand than the code snippet `t` alone, because you also must remember that `a` can't be equal to 0, and so you can be sure that the expression `1 / a` will not crash. The cognitive complexity of the three first lines is equal to ***C<sub>c</sub>(s)***, but the cognitive complexity of the three last lines is strictly higher than ***C<sub>c</sub>(t)***. So, in this example, we have ***C<sub>c</sub>(s + t) > C<sub>c</sub>(s) + C<sub>c</sub>(t)***.

Of course, that's not because this result is true for this example that it will be true for all the possible code snippets. For example, we may think that when the two code snippets are independent, we will have ***C<sub>c</sub>(s + t) = C<sub>c</sub>(s) + C<sub>c</sub>(t)***.


* Example

```ts
// Code snippet s
let a = 2;

// Code snippet t
let b = 3;

// Code snippet s + t
let a = 2;
let b = 3;
```

In this case, the second line is independent of the first one, so we maybe have ***C<sub>c</sub>(s + t) = C<sub>c</sub>(s) + C<sub>c</sub>(t)***, but we could also think that when you read the second line, even if there is no dependence with the first one, you must *remember* that there is no dependence... So, we could again have ***C<sub>c</sub>(s + t) > C<sub>c</sub>(s) + C<sub>c</sub>(t)***.

This result is probably non-demonstrable without experiences in the real world, with enough statistical data to obtain a highly accurate result. It is a *conjecture* and not a *proposition*.




***Work in progress...***
