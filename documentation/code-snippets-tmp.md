
# The set of code snippets

In the [cognitive complexity's definition](cognitive-complexity.md), the concept which is the most well-defined seems to be the notion of *code snippet*. That's probably true, but that doesn't mean that we can neglect to define it accurately. To be able to obtain scientific results, we need at first define precisely each word that we use. What is a *code snippet* ? A *valid code snippet* ? A *program* ? A *system* ? The *state of a system* ? All of these notions are defined more or less accurately in many scientific articles, and their definitions are more or less consensual.

In this project, we will specify our own definitions of simple or complex notions. That doesn't mean that we think that they will be better than the others, but simply that everyone should know accurately what *we* talk about when we use one of these definitions.

## Table of contents

* [Programming language](#programming-language)
* [Basic definitions around code snippets](#basic-definitions-around-code-snippets)
* [Valid code snippets](#valid-code-snippets)
* [References](#references)
* [Roles and descriptions](#roles-and-descriptions)
* [Operations on code snippets](#operations-on-code-snippets)
  * [Addition](#addition)
  * [Propositions and conjectures](#propositions-and-conjectures)


## Programming language

In theoretical computer science, we usually start by defining what is a computer language. In our case, it is not enough general. Our aim goal is to measure the time required for a developer to understand a code snippet, but we also have in mind the idea to measure the time that he will need to debug some program.

How to debug a program, in the real world ? At first, simply by opening files, read them, and try to understand them. Each file is a document containing a text which may have different parts written in different languages. For example, a file may include some `html`, `javascript` and `php` code. That's why, when we'll need to define what is a bug and how to measure the debugging time, we will need a concept larger than a *programming language*. 

In fact, the reality is simple: when a developer opens a file, we only know he that a *text* to read. 

> **Definition**
>
> A ***text*** is a finite set of ordered individual elements, which are the ***characters*** of the text.

* Example

In the text below, `a`, `b` and `c` are characters, but not `ab`, which is not individual: it can be split in `a` + `b`.

```ts
ab c
```

Now, let's remind the main concepts of theoretical computer science :

> **Definition**
>
> A ***programming language*** is a [formal language](https://en.wikipedia.org/wiki/Formal_language) comprising a set of instructions that produce various kinds of output.

The ***alphabet*** of a formal language consists of symbols, letters, or tokens that concatenate into strings of the language. Each string concatenated from symbols of this alphabet is called a ***word***, and the words that belong to a particular formal language are sometimes called ***well-formed words*** or well-formed formulas. 

A formal language is often defined by means of a [formal grammar](https://en.wikipedia.org/wiki/Formal_grammar):

> **Definition**
>
> A ***formal language*** describes how to form strings from a language's alphabet that are valid according to the language's syntax. A grammar does not describe the meaning of the strings or what can be done with them in whatever context—only their form. 
> 
> A ***formal grammar*** is defined as a set of production rules for strings in a formal language.

> **Definition**
>
> The ***syntax*** of a computer language is the set of rules that defines the combinations of symbols that are considered to be correctly structured statements or expressions in that language.

**Remark**

There is a usual debate about the belonging of the markup languages -like HTML- in the set of the formal languages. We will not enter this debate, but as the markup files must be red and understood by developers, they are relevant for the cognitive complexity theory. Thus, we will include them in this set.

Now, we can define what is a *code snippet*:



[-> Top](#the-set-of-code-snippets)
## Basic definitions around code snippets

> **Definition**
>
> A ***code snippet*** is a triplet `(s, L, S)` where `s` is a [text](#programming-language), `L` a [programming language](#programming-language) and `S` a given [system](systems.md).

Thereafter, by abuse of language, we will simply note `s` a code snippet `(s, L, S)`. It will be implicit that a code snippet refers to some computer language `L` and to the system containing `s`. Furthermore, a code snippet is supposed to be written in a single file.

**Remark**

By convention, if `s` is an empty string, the couple `(s, L)` is considered as a code snippet and noted `''`.

**Remark**

A code snippet may be valid or not. It even may contains characters which are not included in the alphabet of `L`.

* Example

```ts
// Code snippet s
ab!z"{-a] =(r|€x
```
With the definition above, the couple (`s`, `TypeScript`) is a code snippet, even if it's not a valid TypeScript code.

Why do we need to have a so large definition of a *code snippet* ? Because we want to know what time will need a developer to understand some code, valid or not. When he will try to debug a TypeScript file, a developer can find a character which is not admitted by this language (and which will cause a syntax error).

> **Definition**
>
> A ***separator*** is an invisible character. Tha characters which are not separators are called the ***visible characters***.

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

> **Definition**
>
> A ***string*** is an ordered set of visible characters of a given code snippet.


> **Definition**
>
> A ***file*** is a quadruplet (p, n, t, L) where `p` is a string which represents its path, `n` is a string which represents its name, `t` its content (*i.e.* the *text* of the file), and `L` is a given programming language.

**Remark**

Of course, in the real world, a file can't be defined with only these 4 elements, but for our purpose, we only need them.

## Valid code snippets

> **Definition**
>
> A ***context-sensitive valid code snippet*** is a code snippet `(s, L)` where `s` respects the [context-sensitive grammar](https://en.wikipedia.org/wiki/Context-sensitive_grammar) of `L`. The set of the context-sensitive valid code snippets of a given language `L` is noted **V**<sup>+</sup>.
>
> A ***valid code snippet*** is a code snippet `(s, L)` where `s` respects the [context-free grammar](https://en.wikipedia.org/wiki/Context-free_grammar) of `L`. The set of the valid code snippets of a given language `L` is noted **V**.
>
> A ***validatable code snippet*** is a code snippet `(s, L)` which can be concatenated with another code snippet to give a valid code snippet. The set of the validatable code snippets of a given language `L` is noted **V**<sup>-</sup>.



* Example 1

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
// Code snippet t
  a = a + 1;
}
```

**Remark**

The concatenation of the two code snippets must not have a letter on the both sides of the merge, like `va` + `r a = 2;`.

> **Proposition**
>
> Each subset of a valid code snippet is a validatable code snippet

This result ensues directly from the definitions of valid and validatable code snippets.

Assuming that every computer language integrates the concept of "line break", we can give the following definition :

> **Definition**
>
> The subset of a code snippet defined by the ordered characters between two consecutive line breaks is called a ***line of code***. If the code snippet has no line break, it has only one line of code which is the code snippet itself.

By definition, each line of code of a valid code snippet is a validatable code snippet.

> **Definition**
>
> Let (p, n, t, L) a given file. The code snippet (t, L) is called a ***module***.

[-> Top](#the-set-of-code-snippets)
## Implementation and behaviors

> **Definition**
>
> An ***implementation*** of a feature *-or a task-* is a set of code snippets which are providing a behavior of the system corresponding to the specs of the feature *-or the task-*.

> **Definition**
>
> The ***behavior*** of a context-sensitive valid code snippet `s` is the [behavior of the system](systems.md) when an external process calls one of the exported references of `s`. We say that `s` is an ***implementation*** of its behavior.

[-> Top](#the-set-of-code-snippets)
## References

> **Definition**
>
> An ***identifier*** is a name chosen by a developer which represents a given data of the program: variables, constants, objects, functions, classes, properties, methods, interfaces, enums, types, etc.
> 
> The couple made up of an identifier and its value is called a ***reference***.


> **Definition**
>
> The ***declaration of a reference*** `r` is the code snippet specifying its name, its type, its parameters if they exist, and its comments if they exist. These comments are also called the ***description*** of `r`.
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

The *declaration* of the reference `getPrice` is:

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

> **Definition**
>
> An ***exported reference*** is a reference declared in a code snippet `s` which is accessible outside of `s`.
> 
> An ***imported reference*** located in a code snippet `s` is a reference declared outside of `s`.

**Examples**
  
Assuming that each file may be called by some other part of the program, a [module](#valid-code-snippets) is by definition an exported reference. 

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

> **Definition**
>
> The ***behavior of a reference*** `r` is the [behavior of the system](systems.md) when `r` is initialized, modified or called.

**Remark**

* The definition of the behavior of a reference includes the variations of its value, and its impact on the rest of the system, *i.e.* its side effects.

[-> Top](#the-set-of-code-snippets)
## Roles and descriptions

When a task is transmitted to a developer, he will write some code snippets, in the aim to provide the expected behavior of the system, in the conditions given by the specs. For that, he will code some references, which will be exposed to the rest of the application, or to the rest of the world in the case of a public library. Each of these external references has a specific *role* to play in the aim to provide the expected behavior of the system in the context specified by the task.

> **Definition**
>
> The ***role of a reference*** `r` is the behavior of `r` expected by its author when `r` is used by any code snippet.
>
> The ***role of a reference `r` in the context of a valid code snippet `s`*** is the behavior of `r` expected by its author if he had written `s`.

**Remark**

* The role of a reference is a subjective notion. It is something which is in the mind of the author of the code snippet.

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



[-> Top](#the-set-of-code-snippets)
## Operations on code snippets

### Addition

#### Definition of the addition
> **Definition**
>
> We call **S<sub>L</sub>** the set of the *code snippets* of a given formal language `L`, with the concatenation operation noted `+`.
>
> We call **V<sub>L</sub>**<sup>-</sup> the subset of **S<sub>L</sub>** defined by the set of the *validatable code snippets* of a given formal language `L`, with the concatenation operation noted `+`.
>
> We call **V<sub>L</sub>** the subset of **V<sub>L</sub>**<sup>-</sup> defined by the set of the *valid code snippets* of a given formal language `L`, with the concatenation operation noted `+`.
>
> We call **V<sub>L</sub>**<sup>+</sup> the subset of **V<sub>L</sub>** defined by the set of the *context-sensitive code snippets* of a given formal language `L`, with the concatenation operation noted `+`.

**Notation**

For the sake of simplification, when the specification of the language is not needed, we will simply note **S**, **V**<sup>-</sup>, **V** and **V**<sup>+</sup> the sets of code snippets, validatable code snippets, valid code snippets and context-sensitive code snippets of an implicit programming language **L**. 

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



[-> Top](#the-set-of-code-snippets)
#### Propositions and conjectures


> **Conjecture**
>
> The cognitive complexity of the sum of two code snippets is strictly higher than the sum of the cognitive complexity of each of them.
> ```ts
> Cc(s + t) > c(s) + c(t)
> ```

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
In the example above, when you read the code snippet `s + t`, the cognitive complexity of the three first lines is the same as the complexity of `s`, because you have exactly the same information to understand. At the opposite, the three last lines will take more time to understand than the code snippet `t` alone, because you also must remember that `a` can't be equal to 0, and so you can be sure that the expression `1 / a` will not crash. The cognitive complexity of the three first lines is equal to `Cc(s)`, but the cognitive complexity of the three last lines is strictly higher than `Cc(t)`. So, in this example, we have `Cc(s + t) > Cc(s) + Cc(t)`.

Of course, that's not because this result is true for this example that it will be true for all the possible code snippets. For example, we may think that when the two code snippets are independent, we will have `Cc(s + t) = Cc(s) + Cc(t)`.


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

In this case, the second line is independent of the first one, so we maybe have `Cc(s + t) = Cc(s) + Cc(t)`, but we could also think that when you read the second line, even if there is no dependence with the first one, you must *remember* that there is no dependence... So, we could again have `Cc(s + t) > Cc(s) + Cc(t)`.

This result is probably non-demonstrable without experiences in the real world, with enough statistical data to obtain a highly accurate result. It is a *conjecture* and not a *proposition*.




***Work in progress...***
