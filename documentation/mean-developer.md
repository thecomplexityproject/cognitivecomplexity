[<-](README.md)
# Mean developer

## Table of contents

* [Introduction](#introduction)

[<- Top](#mean-developer)
## Introduction

The definition of the [cognitive complexity](./cognitive-complexity.md) uses the term `mean developer`. We need to accurate what is exactly a `mean developer` to be able to calculate objectively the cognitive complexity of a given code snippet. In other words, we need to precise what are the characteristics of a developer which are correlated to the notion of cognitive complexity.

##### -> Skill
> **Definition**
>
> We call ***skill*** a technical aptitude that can be acquired by a human being.


##### -> Programming skill
> **Definition**
>
> We call ***programming skill*** a skill in relation with programming. We note ***S<sub>k</sub>*** the set of all the possible programming skills.


##### -> Developer
> **Definition**
>
> A ***developer*** is defined by a couple `(h, S)` where `h` represents a human being and `S` a non-empty set of programming skills acquired by `h`. `S` is a subset of ***S<sub>k</sub>***.

**Remark**

* A developer, as human being, has many characteristics which may affect the time he needs to understand some code snippet.


##### -> Domain of knowledge
> **Definition**
>
> A ***programming knowledge*** is a domain of knowledge in relation with programming which can be learned or mastered by a human being.

**Examples**

* Algorithmic
* Design patterns
* Specific programming language
* Specific framework
* Specific IDE

**Remark**

* By definition, a programming skill is obtained by acquiring or improving some programming knowledge. Thus, a developer is a human being which acquired at least a programming knowledge.


##### -> Understanding speed
> **Definition**
>
> The ***understanding speed*** by a given developer `d` of a given code snippet `s` is equal to the cognitive complexity of `s` divided by the time needed by `d` to understand it. We note it ***S<sub>d</sub>(s)***
> 
> In other words, ***S<sub>d</sub>(s)* = *C<sub>c</sub>(s) / t***, where `t` is the time needed by `d` to understand `s`.

***Work in progress...***
