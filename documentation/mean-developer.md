[<-](README.md)
# Mean developer

## Table of contents

* [Introduction](#introduction)

[<- Top](#mean-developer)
## Introduction

The definition of the [cognitive complexity](./cognitive-complexity.md) uses the term *"mean developer"*. We need to accurate what is exactly a *"mean developer"* to be able to calculate objectively the cognitive complexity of a given code snippet. In other words, we need to precise what are the characteristics of a developer which are correlated to the notion of cognitive complexity.

[<- Top](#mean-developer)
## Skills

##### -> Skill
> **Definition**
>
> We call ***skill*** a technical aptitude that can be acquired by a human being. A skill may be *quantified*, *measured* or *estimated*. This quantification, measure or estimation is called a ***level of skill***. 

**Examples**

* Mastering a foreign language (estimated with exams or tests)
* Mastering a programming language (estimated with exams or tests)
* Mastering a tool (estimated with exams or tests)


##### -> Measured skill
> **Definition**
>
> Let `d` a developer.
> We call ***measured skill*** a couple `(s, l)` where `s` is a skill mastered by `d` with a level equal to `l`.

##### -> Human factor
> **Definition**
> 
> A ***human factor*** is a human characteristic which may be *correlated* with some levels of skills.

**Examples**

* Experience
* Age
* Education
* Career path
* ...

##### -> Programming skill
> **Definition**
>
> We call ***programming skill*** a skill in relation with programming. We note ***S<sub>k</sub>*** the set of all the possible programming skills. For simplicity, thereafter, the word *skill* will always imply that we talk about *programming skill*.

**Examples**

* Algorithmic
* Design patterns
* Specific programming language
* Specific framework
* Specific IDE


[<- Top](#mean-developer)
## Developers

##### -> Developer
> **Definition**
>
> A ***developer*** is defined by a couple `(h, S)` where `h` represents a human being and `S` a non-empty set of programming skills acquired by `h`. `S` is a subset of ***S<sub>k</sub>***.

**Remark**

* By definition, a programming skill is obtained by acquiring or improving some programming knowledge. Thus, a developer is a human being which acquired at least a programming knowledge.


##### -> Time of understanding
> **Definition**
>
> Let `d` a developer and `s` a code snippet.
> The ***time of understanding*** of `s` by `d` is the time needed by `d` to understand `s`.


##### -> Understanding speed
> **Definition**
>
> The ***understanding speed*** by a given developer `d` of a given code snippet `s` is equal to the cognitive complexity of `s` divided by the time needed by `d` to understand it. We note it ***S<sub>d</sub>(s)***
>
> In other words, ***S<sub>d</sub>(s)* = *C<sub>c</sub>(s) / t***, where `t` is the time needed by `d` to understand `s`.

[<- Top](#mean-developer)
## The mean developer

Our ultimate goal is to measure the cognitive complexity of a code snippet `s`. To be able to do that, we must use the notion of *mean developer*, which is intuitively a developer which has enough programming knowledge to understand `s`, but which is not necessarily an expert in the programming language. We want to know the time needed by a *"classic"* developer to understand `s`. 

A client or a manager needs to know what will be *approximately* the time needed by his developers to maintain the code, fix bugs or develop new features. For that, he needs an approximate value, an estimation of this duration for a *mean developer*. With this value, he will be able to estimate the time needed for *his developers*, knowing for example if they are senior or junior developers. 

That's why we need to specify what *"mean developer"* exactly means.

### Criteria to be taken into account

What are the criteria to be taken into account ? What should we assume, and what we should not ?

At first, we should assume that the developer has the minimal programming skills to be able to understand the code snippet. We must assume that he has the minimum level of skills allowing him to understand a code snippet of moderate difficulty without being obstructed by a lack of knowledge. 


##### -> Minimal skill relative to a code snippet
> **Definition**
>
> Let `s` a given code snippet. We call ***minimal skill relative to `s`*** a skill which is mandatory with a minimum level `l` to be able to understand `s`. The set of the minimal skills relative to `s` is noted ***S<sub>k</sub><sup>s</sup>***.

**Remark**

* A minimal skill is always relative to a given code snippet. For example, if this code snippet is written in JavaScript, the set of minimal skills must include a minimal level of skill in the mastering of JavaScript.

**Examples of minimal skills**

For any code snippet `s`, the set of minimal skills  must include the following elements :

* Algorithmic
* General knowledge in programming
* Specific knowledge in the programming language of `s`
* Specific knowledge in the framework used by the application using `s`
* Mastering of an IDE 

**Remark**

Most of the developers are mastering an IDE, which helps them significantly to increase their productivity. For example, a hovering of the mouse on the identifier of a function may display its signature, and a click on it may open the file containing this function and display its implementation. These features helping considerably the developers to understand the code, we must take this knowledge into account.


[comment]: <> (##### -> Maximal skill relative to a code snippet)

[comment]: <> (> **Definition**)

[comment]: <> (>)

[comment]: <> (> Let `t` a code snippet, and `&#40;s, l&#41;` the couple defining a minimal skill relative to `t`. We call ***maximal skill relative to `s`*** a skill which is mandatory with a minimum level `l` to be able to understand `s`. The set of the minimal skills relative to `s` is noted ***S<sub>k</sub><sup>s</sup>***.)



***Work in progress...***
