# Cognitive Complexity

## Definition of the cognitive complexity

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

## Definition of the cognitive complexity metric

The cognitive complexity metric could be defined like this :

> **Definition**
>
> We call ***cognitive complexity metric*** the function which assigns to each code snippet its cognitive complexity. This metric is noted ***Cc***.
>
> If ***S*** is the set of code snippets and ***R<sup>+</sup>*** the set of the real positive numbers, we have
> ```ts
> Cc:  S   ->   R+
>     s   ->   cognitiveComplexity(s)
> ```
