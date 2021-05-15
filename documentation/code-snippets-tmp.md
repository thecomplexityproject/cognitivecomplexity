
# The set of code snippets

In the [cognitive complexity's definition](cognitive-complexity.md), the concept which is the most well-defined seems to be the notion of *code snippet*. That's probably true, but that doesn't mean that we can neglect to define it accurately. To be able to obtain scientific results, we need at first define precisely each word that we use. What is a *code snippet* ? A *valid code snippet* ? A *program* ? A *system* ? The *state of a system* ? All of these notions are defined more or less accurately in many scientific articles, and their definitions are more or less consensual.

In this project, we will specify our own definitions of simple or complex notions. That doesn't mean that we think that they will be better than the others, but simply that everyone should know accurately what *we* talk about when we use one of these definitions.

## Table of contents

* [Programming language](#programming-language)
* [Basic definitions around code snippets](#basic-definitions-around-code-snippets)
* [References, roles, descriptions and features](#references-roles-and-descriptions)
  * [References](#references)
  * [Behaviors, roles and descriptions](#behaviors-roles-and-descriptions)
  * [Features](#features)
* [Operations on code snippets](#operations-on-code-snippets)
  * [Addition](#addition)


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
### Features

> **Definition**
>
> A ***feature*** is a set of functionalities provided by the [system](code-snippets.md) to the users.

> **Definition**
>
> An ***implementation*** of a feature is a set of code snippets of a given [program](code-snippets.md) which are able to provide this feature to the users.

> **Definition**
>
> A ***prime contractor*** is a natural or legal person which is asking a natural or legal person to program a given set of features.
> 
> An ***intermediate contractor*** is a natural or legal person which is working under the orders of a prime contractor or another intermediate contractor in the aim to develop a code snippet, a feature or a set of features wanted by the prime contractor.

**Examples**

Subcontractor companies, product managers, architects and lead developers are intermediate contractors.


> **Definition**
>
> The ordered set of natural or legal persons between the prime contractor and a given developer, including them, is called a ***chain of responsibilities***.

> **Definition**
>
> The ***specs*** are the set or instructions describing the expected [behavior of the system](systems.md) for a given feature, which are transmitted by the prime contractor.  



[-> Top](#the-set-of-code-snippets)
## References, roles and descriptions

### References

> **Definition**
>
> An ***exported reference*** is an object declared in a code snippet `s` which is accessible outside of `s`.
> 
> An ***imported reference*** located in a code snippet `s` is an object referring to an external reference of another code snippet `t`.

**Examples**
  
Variables, constants, functions, classes, interfaces, enums, types... may be exported or imported references.

Assuming that each file may be called by some other part of the program, a [module](#valid-code-snippets) is by definition an exported reference. 

### Behaviors, roles and descriptions

> **Definition**
>
> The ***behavior*** of a context-sensitive valid code snippet `s` is the [behavior of the system](systems.md) when an external process calls one of the exported references of `s`. We say that `s` is an ***implementation*** of its behavior.

> **Definition**
>
> The ***role of a context-sensitive valid code snippet*** `s` is the [behavior of the system](systems.md) expected by the author of `s` when another code snippet calls one of the exported references of `s`.

**Remark**

With this definition, a *role* is clearly a subjective notion. It is something which is in the real world, not in the theoretical world. A *role* is in the *world of measurability*, a behavior is in the *world of computability*. The border between these two worlds is located between the concepts of *role* and *behavior*.


> **Definition**
>
> The ***description*** of the role `r` of a code snippet `s` is the set of elements written by the author of `s` which are describing its role.

Examples of kinds of descriptions of a role `r` :
* the name of `r`
* the signature relative to `r` (for functions and methods)
* the comments relative to `r`

**Example**

```ts
// Code snippet s
interface Profile {
	address?: string;
	firstName: string;
	lastName: string;
}

/**
 * Returns the profile corresponding to a given id
 * @param id
 */
function getProfile(id: number): Profile {
	const data: ProfileEntity = getProfileFromDataBase(id);
	const profile = {
		firstName: data.firstName,
        lastName: data.lastName
    };
}
```

Let `d` the developer which wrote `s`, and assume that for him, the role of the function `getProfile()` is to return the profile located in database corresponding to the given `id`. The description of this role is specified by the name of the function (`getProfile`) and by the comments above this function.

Now, let `d'` another developer which will use `getProfile()`. He thinks that the role of this function is to return the profile located in database corresponding to the given `id`.

```ts
// Code snippet t
function getProfileAddress(idProfile: number): string {
	const profile: Profile = getProfile(id);
	return profile.address;
}
```

And... there is a bug ! Why ? Because in the mind of `d`, `getProfile()` returns only the firstname and lastName fields, not the address. On the other side, `d'` thought that the field *address* will be included. Thus, the code snippet written by `d'` will have a behavior which not corresponds to the role ha wants to give to its function `getProfileAddress()`. It is the exact definition of a [bug](bugs.md#definition-of-a-bug).

But who is guilty ? `d` or `d'` ? It is not so clear.

Assume that `d` wrote its code six months ago, at a time when it was clear for everyone that his function `getProfile()` will return only the firstname and lastName. At that time, the program was running correctly, there was no bug. Today, someone asked `d'` to write a code returning the address of a given profile. At this moment, `d'` will create a bug, because he will write a code snippet with a behavior which does not correspond to the role he wants to give to its function. 

`d'` is he the only one which is guilty ? In reality, `d` has its part of responsibility, because he wrote a *description* which was not exactly describing the behavior of `getProfile()`. He misled `d'`. Consequently, he increased unnecessarily the cognitive complexity of `getProfile()`: with its bad quality definition, `getProfile()` was more difficult to understand. In other words,the cognitive complexity of the exported reference `getProfile()` could be reduced with a refactor `r` like this:


```ts
// Code snippet r(s)
interface Profile {
	address?: string;
	firstName: string;
	lastName: string;
}

/**
 * Returns the firstName and the lastName of a Profile corresponding to a given id
 * @param id
 */
function getProfile(id: number): Profile {
	const data: ProfileEntity = getProfileFromDataBase(id);
	const profile = {
		firstName: data.firstName,
        lastName: data.lastName
    };
}
```


> **Definition**
>
> The ***role of a reference*** `r` is the expected [behavior of the system](systems.md) when a process calls `r`, in terms of the developer which *wrote* the implementation of `r`.


**Remark**

When `s` is a module, `s` is considered itself as one of its exported references.

**Remark**

The quality of the description of a reference `r` is measured by the relation of correlation between its role, and the role predicted by other developers calling `r`.

> **Definition**
>
> The ***quality level*** of a description of an exported reference `r` is said to be:
> * ***high*** if a mean developer is able to understand the role of `r` with only the name of `r` (and its signature for functions)
> * ***medium*** if a mean developer is able to understand the role of `r` with the name of `r`, its signature and its comments
> * ***low*** if a mean developer is able to understand the role of `r` with the name of `r`, its signature, its comments and its implementation

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
In the example above, when you read the code snippet `s + t`, the cognitive complexity of the three first lines is the same as the complexity of `s`, because you have exactly the same information to understand. At the opposite, the three last lines will take more time to understand than the code snippet `t` alone, because you also must remember that `a` can't be equal to 0, and so you can be sure that the expression `1 / a` will not crash. The cognitive complexity of the three first lines is equal to `c(s)`, but the cognitive complexity of the three last lines is strictly higher than `c(t)`. So, in this example, we have `c(s + t) > c(s) + c(t)`.

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
