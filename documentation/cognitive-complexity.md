# Cognitive Complexity

## Definition

> **Definition**
> 
> The ***cognitive complexity*** of a code snippet is the time required by a developer to understand it.

This definition is simple to understand and clarifies what we should measure: a duration. However, this definition has some ambiguities:

* What is a *code snippet* ?
* How to define a *developer* ?
* What do we mean by *understand* ?

These questions are studied in specific pages :

* [The set of code snippets](code-snippets.md)
* [The mean developer](mean-developer.md)
* [The understanding](understanding.md)

Thanks to the clarification of these concepts, we will be able to define experimental protocols which could be enough consensual to be used by the entire scientific community in the aim to collect comparable data.

* [Experimental protocols](experimental-protocols.md)

## Propositions and conjectures

Some results result directly from the definition of the different concepts described in this documentation. We call them ***propositions***.

Other results are probably true, but must be calculated or measured in the real world. These results needs the help of experimental studies to demonstrate their validity. We call them ***conjectures***.

> **Definition**
>
> We call ***c*** the function which assigns to each code snippet its cognitive complexity.
> 
> If ***S*** is the set of code snippets and ***R<sup>+</sup>*** the set of the real positive numbers, we have
> ```ts
> c:  S   ->   R+
>     s   ->   cognitiveComplexity(s)
> ```
 

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

