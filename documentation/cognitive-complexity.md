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
* [The mean developer]
* [The understanding]

With the help of these clarified concepts, we will be able to define experimental protocols which could be enough consensual to be used by the entire scientific community in the aim to collect comparable data.

* [Experimental protocols]

## Propositions and conjectures

Some results result directly from the definition of the different concepts described in this documentation. We call them ***propositions***.

Other results are probably true, but must be calculated or measured in the real world. These results needs the help of experimental studies to demonstrate their validity. We call them ***conjectures***.

> **Definition**
>
> We call ***c*** the function which assigns to each code snippet its cognitive complexity.
> In other words, if ***S*** is the set of code snippets and ***R<sup>+</sup>*** the set of the real positive numbers, we have
> ```ts
> c:  S   ->   R+
>     s   ->   cognitiveComplexity(s)
> ```
 

> **Proposition**
> 
> The cognitive complexity of the sum of two valid code snippets is strictly higher than the sum of the cognitive complexity of each of them.
> 
* Example

