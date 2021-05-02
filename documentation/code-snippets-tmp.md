# The set of code snippets

In the [cognitive complexity's definition](.cognitive-complexity.md), the concept which is the most well-defined seems to be the notion of *code snippet*. That's probably true, but that doesn't mean that we can neglect to define it accurately. To be able to obtain scientific results, we need at first define precisely each word that we use. What is a *code snippet* ? A *valid code snippet* ? A *program* ? A *system* ? The *state of a system* ? All of these notions are defined more or less accurately in many scientific articles, and their definitions are more or less consensual.

In this project, we will explicit our own definitions of simple or complex notions. That doesn't mean that we think that they will be better than the others, but simply that everyone should know accurately what *we* talk about when we use one of these definitions.

## Table of contents

* [Computer language](#computer-language)
* [Code snippets](#code-snippets)




## Computer language

Let's start by the beginning: the definition of a computer language :

> **Definition**
>
> A ***computer language*** is defined by an alphabet, a vocabulary, [syntactic rules](https://en.wikipedia.org/wiki/Programming_language#Syntax) and [semantic rules](https://en.wikipedia.org/wiki/Programming_language#Semantics).

Now, we can define what is a *code snippet*.






## Code snippets

> **Definition**
>
> A ***code snippet*** is a couple `(s, L)` where `s` is a set of ordered characters of the alphabet of a given computer language `L`.

Thereafter, by abuse of language, we will simply note `s` a code snippet `(s, L)`. It will be implicit that a code snippet refers to some computer language `L`.

* Example

The code below is written in the TypeScript alphabet, so it is a code snippet with the definition above.
```ts
// Code snippet s
ab!z"{-a] =(r|x
```

**Remark**

In the definition above, the set of characters `s` is supposed to be written in only one document (a file).

> **Definition**
>
> A ***valid code snippet*** is a code snippet `(s, L)` where `s` respects the vocabulary and the syntactic rules of `L`.

* Example

The code below is written in the TypeScript vocabulary and respects its syntax, so it is a valid code snippet.
```ts
// Code snippet t
if (a > 0) {
    a = a + 1;
}
```

> **Definition**
>
> An ***executable code snippet*** is a valid code snippet `(s, L)` where `s` respects the semantic rules of `L`.

* Example

The code below is written in the TypeScript vocabulary and respects its syntax, so it is a valid code snippet.
```ts
// Code snippet u
let a: number;
if (a > 0) {
    a = a + 1;
}
```

**Remark**

The code snippet `t` above is not an executable code snippet because the variable `a` was not defined before the line `if (a > 0)`.

> **Definition**
>
> A ***module*** is the code snippet containing all the characters of a given file.

Assuming that every computer language integrates the concept of "line break", we can give the following definition :


> **Definition**
>
> The subset of a code snippet defined by the ordered characters between two consecutive line breaks is called a ***line of code***. If the code snippet has no line break, it has only one line of code which is the code snippet itself.






## Addition of two code snippets

> **Definition**
>
> We call **S** the couple `(S, +)` where `S` is the set of all the possible code snippets of a given language, and `+` is defined by the concatenation operation.
>
> We call **V** the subset of `(S, +)` defined by all the possible valid code snippets of a given language.
>
> We call **E** the subset of `(V, +)` defined by all the possible executable code snippets of a given language.

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



