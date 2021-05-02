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

* [The set of code snippets](code-snippets-tmp.md)
* [The mean developer](mean-developer.md)
* [The understanding](understanding.md)

We should also define the cognitive complexity metric :

> **Definition**
>
> We call ***c*** the function which assigns to each code snippet its cognitive complexity.
>
> If ***S*** is the set of code snippets and ***R<sup>+</sup>*** the set of the real positive numbers, we have
> ```ts
> c:  S   ->   R+
>     s   ->   cognitiveComplexity(s)
> ```

Thanks to the clarification of these concepts, we will be able to define experimental protocols which could be enough consensual to be used by the entire scientific community in the aim to collect comparable data.

* [Experimental protocols](experimental-protocols.md)


## Propositions and conjectures

Some results result directly from the definition of the different concepts described in this documentation. We call them ***propositions***.

Other results are probably true, but must be calculated or measured in the real world. These results needs the help of experimental studies to demonstrate their validity. We call them ***conjectures***.
