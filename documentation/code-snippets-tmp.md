# Temp

# The set of code snippets

In the [cognitive complexity's definition](.cognitive-complexity.md), the concept which is the most well-defined seems to be the notion of *code snippet*. That's probably true, but that doesn't mean that we can neglect to define it accurately. To be able to obtain scientific results, we need at first define precisely each word that we use. What is a *code snippet* ? A *valid code snippet* ? A *program* ? A *system* ? The *state of a system* ? All of these notions are defined more or less accurately in many scientific articles, and their definitions are more or less consensual.

In this project, we will specify our own definitions of simple or complex notions. That doesn't mean that we think that they will be better than the others, but simply that everyone should know accurately what *we* talk about when we use one of these definitions.

## Table of contents

* [Programming language](#programming-language)
* [Code snippets](#code-snippets)
* [Addition of two code snippets](#addition-of-two-code-snippets)
* [Propositions and conjectures](#propositions-and-conjectures)
* [Systems](#systems)


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
> A ***programming language*** is a formal language comprising a set of instructions that produce various kinds of output.

The ***alphabet*** of a formal language consists of symbols, letters, or tokens that concatenate into strings of the language. Each string concatenated from symbols of this alphabet is called a ***word***, and the words that belong to a particular formal language are sometimes called ***well-formed words*** or well-formed formulas. 

A formal language is often defined by means of a formal grammar:

> **Definition**
>
> A ***formal language*** describes how to form strings from a language's alphabet that are valid according to the language's syntax. A grammar does not describe the meaning of the strings or what can be done with them in whatever context—only their form. 
> 
> A formal grammar is defined as a set of production rules for strings in a formal language.

> **Definition**
>
> The ***syntax*** of a computer language is the set of rules that defines the combinations of symbols that are considered to be correctly structured statements or expressions in that language.

Now, we can define what is a *code snippet*:





[-> Top](#the-set-of-code-snippets)
## Code snippets

> **Definition**
>
> A ***code snippet*** is a couple `(s, L)` where `s` is a [text](#programming-language) and `L` a [programming language](#programming-language).

Thereafter, by abuse of language, we will simply note `s` a code snippet `(s, L)`. It will be implicit that a code snippet refers to some computer language `L`. Furthermore, a code snippet is supposed to be written in a single file.

**Remark**

By convention, even if `s` is the empty string `''`, the couple `(s, L)` is also a code snippet.

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
> A ***file*** is a quadruplet (p, n, t, L) where `p` represents its path, `n` its name, `t` its content (*i.e.* the *text* of the file), and `L` is a given programming language.

**Remark**

Of course, in the real world, a file can't be defined with only these 4 elements, but for our purpose, we only need them.


> **Definition**
>
> A ***context-sensitive valid code snippet*** is a code snippet `(s, L)` where `s` respects the [context-sensitive grammar](https://en.wikipedia.org/wiki/Context-sensitive_grammar) of `L`.
>
> A ***context-free valid code snippet*** is a code snippet `(s, L)` where `s` respects the [context-free grammar](https://en.wikipedia.org/wiki/Context-free_grammar) of `L`.

* Example

```ts
// Code snippet t
if (a > 0) {
    a = a + 1;
}
```
`t` is a *context-free valid code snippet*, but not a *context-sensitive valid code snippet*, because `a` is not defined in `t`.

> **Definition**
>
> For the sake of simplification, we will simply call ***valid code snippet*** a *context-free valid code snippet*.

> **Definition**
>
> Let (p, n, t, L) a given file. The code snippet (t, L) is called a ***module***.

Assuming that every computer language integrates the concept of "line break", we can give the following definition :


> **Definition**
>
> The subset of a code snippet defined by the ordered characters between two consecutive line breaks is called a ***line of code***. If the code snippet has no line break, it has only one line of code which is the code snippet itself.






[-> Top](#the-set-of-code-snippets)
## Operations on code snippets

### Addition

> **Definition**
>
> We call **S<sub>L</sub>** the set of the code snippets of a given formal language `L` with the concatenation operation noted `+`.
>
> We call **V<sub>L</sub>** the subset of **S<sub>L</sub>** defined by the set of the code snippets of a given formal language `L` with the concatenation operation noted `+`.
>
> We call **V<sub>L</sub>**<sup>*</sup> the subset of **V<sub>L</sub>** defined by the set of the context-sensitive code snippets of a given formal language `L` with the concatenation operation noted `+`.

**Remark**

The concatenation of two code snippets is a code snippet, so the operation `+` is a function from (**S** x **S**) to **S**.
```
+ : (S x S)              ->    S
    'Hello' + ' world'   =     'Hello world'
```

> **Proposition**
>
> The operation `+` is an internal operation of **V**. In other words, if `s` and `t` are two valid code snippets, then `s + t` is a valid code snippet.
>
**Demonstration**

This result is trivial : if `s` and `t` are two code snippets respecting syntactic rules of a given language `L`, then `s + t` will respect them too.


> **Proposition**
>
> The operation `+` is not an internal operation of **E**: if `s` and `t` are two executable code snippets, then `s + t` may not be executable.
>
**Demonstration**

In TypeScript, assume that we have the code snippets `s` and `t` below :

```ts
// Code snippet s
let a = 2;

// Code snippet t
let a = 3;
```

The code snippet `s + t` is not valid, because the variable `a` will be declared two times :
```ts
// Code snippet s + t
let a = 2;
let a = 3;
```

**Remark**

By contrast, the sum of two non-executable code snippets may be an executable code snippet.

*Example in TypeScript*

```ts
// Code snippet "s"
let a: number;
let b: number;
if (a > 0) {

// Code snippet "t"
b = 2; }
```
`s` and `t` are valid but not executable, and `s + t` is valid :

```ts
// Code snippet "s + t"
let a: number;
let b: number;
if (a > 0) { b = 2; }
```





[-> Top](#the-set-of-code-snippets)
## Propositions and conjectures


> **Conjecture**
>
> The cognitive complexity of the sum of two code snippets is strictly higher than the sum of the cognitive complexity of each of them.
> ```ts
> c(s + t) > c(s) + c(t)
> ```

The main reason of this result is that when you read the second snippet, you must remember what happened in the first one, so the time that you need to understand it is strictly higher than the time that would need if this code snippet was alone.

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

Of course, that's not because this result is true for this example that it will be true for all the possible code snippets. For example, we may think that when the two code snippets are independent, we will have `c(s + t) = c(s) + c(t)`.


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

In this case, the second line is independent of the first one, so we maybe have `c(s + t) = c(s) + c(t)`, but we could also think that when you read the second line, even if there is no dependance with the first one, you must *remember* that there is no dependence... And so, we could again have `c(s + t) > c(s) + c(t)`.

This result is probably non-demonstrable without experiences in the real world, with enough statistical data to obtain a highly accurate result. That's why we call it a *conjecture* and not a *proposition*.






[-> Top](#the-set-of-code-snippets)
## Systems

> **Definition**
>
> We call ***system*** the triplet (H, S, D) corresponding to a functional set, where H is a hardware, S is a software, and D some data.


> **Definition [<sup>w</sup>](https://en.wikipedia.org/wiki/Information_system)**
>
> The term ***hardware*** refers to machinery and equipment. In a modern information system, this category includes the computer itself and all of its support equipment. The support equipment includes input and output devices, storage devices and communications devices.

> **Definition [<sup>w</sup>](https://en.wikipedia.org/wiki/Information_system)**
>
> The term ***software*** refers to computer programs defined as the machine-readable instructions that direct the circuitry within the hardware parts of the system to function in ways that produce useful information from data.
>
> Thereafter, we will simply call ***program*** the set of machine-readable instructions of a given system. In other words, the program is the set of the modules of the software.

> **Definition [<sup>w</sup>](https://en.wikipedia.org/wiki/Information_system)**
>
> ***Data*** are facts that are used by systems to produce useful information. In modern information systems, data are generally stored in machine-readable form on disk until the computer needs them.

By nature, a system evolves over time as a result of the current processes running on it, and because of the eventual inputs received from out of the system.

> **Definition**
>
> A ***process*** is a triplet `(S, l, p)` where `l` is the instruction currently executed by a processor `p` in a given system `S`.


> **Definition**
>
> The ***state of the system*** `S` is the couple `(D, P)` where `D` represents the data of the system and `P` the set of processes running at a time `t`.

With this definition, we are now able to accurate what is the *[understanding](understanding.md)* in our definition of the [cognitive complexity](cognitive-complexity.md)

