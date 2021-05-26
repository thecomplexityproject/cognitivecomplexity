[<-](README.md)
# Mean developer

## Table of contents

* [Introduction](#introduction)

[<- Top](#mean-developer)
## Introduction

The definition of the [cognitive complexity](cognitive-complexity.md) uses the term *"mean developer"*. We need to accurate what is exactly a *"mean developer"* to be able to calculate objectively the cognitive complexity of a given code snippet. In other words, we need to precise what are the characteristics of a developer which are correlated to the notion of cognitive complexity.

[<- Top](#mean-developer)
## Skills

##### -> Skill
> **Definition**
>
> A ***competence*** is a set of knowledge which may be mastered by a human being.

**Examples**

* A foreign language
* Algorithmic
* The computer programming (generally speaking)
* The computer programming (in a specific language)
* A framework
* Design patterns
* A tool or a set of tools (some IDE, for example)

**Remark**

* Thereafter, the word *"competence"* will always imply that we talk about a *programming competence*.

##### -> Skill
> **Definition**
>
> We call ***skill*** a technical aptitude that can be acquired by a human being in the aim to master a competence. 
> 
> A skill may be *quantified*, *measured* or *estimated*. This quantification, measure or estimation is called a ***level of skill***. 

**Remark**

* Thereafter, the word *skill* will always imply that we talk about a *programming skill*. We note ***S<sub>k</sub>*** the set of all the possible programming skills.


##### -> Measured skill
> **Definition**
>
> Let `d` a developer.
> We call ***measured skill*** a couple `(s, l)` where `s` is a skill mastered by `d` with a level equal to `l`.


[<- Top](#mean-developer)
## Developers

##### -> Human factor
> **Definition**
> 
> A ***human factor*** is a human characteristic which may be *correlated* with some levels of skills.

**Examples**

* Age
* Education
* Career path
* ...

##### -> Experience
> **Definition**
>
> We call ***experience*** a couple `(c, t)`, where `c` is a competence and `t` the time spent by a human being to learn `c`.

**Remark**

* By definition, the experience is a human factor.

##### -> Developer
> **Definition**
>
> A ***developer*** is defined by a couple `(h, E)` where `h` represents a human being and `E` his set of experiences.

**Remark**

* By definition, a skill is obtained by acquiring or improving some competence. Thus, a developer is a human being which acquired at least a programming competence thanks to his experiences.


[<- Top](#mean-developer)
## Experience and skills

##### -> Recent experience
> **Definition**
>
> The ***recent experience*** of a developer `d` in a competence `c` is a couple `(t, p)`, where `t` represents time that `d` spent to learn or practiced `c` during a given period `p` (the period preceding the reading of the code snippet, for example).

**Remark**

* `t` and `p` are durations, expressed in time units.

##### -> Stack
> **Definition**
>
> The ***stack*** of a code snippet `s` is the set of fields of competences which are mandatory to understand `s` in the context of the program containing `s`.
> 
> More generally, the ***stack of a set `S` of code snippets*** is the set of fields of competences which are mandatory to understand each element of `S`. The stack of a project, product or program `p` is the stack of all the code snippets of `p`. 

**Example**

* The stack MEAN (MongoDB, Express, Angular, NodeJs) is a stack of Angular webapps. However, some elements of this stack are undertones, like the languages which must be mastered by the developers: JavaScript, TypeScript, HTML, CSS, SQL, and probably other tools, like Mongoose or TypeORM, for example. 
* When some parts of a program `p` may be completely decoupled, a developer may master only some parts of the stack of `p` to understand a given code snippet. It is true for web apps: the front-end developer does not need to master SQL, MongoDB or TypeORM, for example. The stack of the front-end part of `p` is: TypeScript, HTML, CSS, Angular.


##### -> Minimal experience
> **Definition**
>
> The ***minimal experience*** in a competence `f` is an arbitrary couple of numbers `(t, p)` which represents the recent experience that a human being must spend to learn the basics of `f`.
> 
> In the same way, the ***minimal experience in a stack*** `s` is the set of minimal experiences relative to each competence of `s`.


**Remark**

* This couple `(t, p)` is arbitrary. It is a *"threshold"* which is defined in the aim to avoid the cases which could distort the calculations. For example, if a developer has absolutely no knowledge in TypeScript and JavaScript, he will need an extremely long time to understand any Angular code snippet. This case could drastically distort the calculation of the cognitive complexity of this code snippet. That's why we need to define this threshold, which represents the time that a developer will need to learn the basics of the stack of the code snippet he reads.

**Example**

We could say that the minimal experience in the stack "JavaScript" is :
  - 1 year of computer programming during the last 5 years
  - 1 month of programming in JavaScript during the last 6 months 
    
With this definition of the *minimal experience in JavaScript*, we can be sure that a developer having this minimal experience will not need days or weeks to understand a JavaScript code snippet of medium difficulty. This threshold will help us to make average calculations avoiding extreme cases which could distort the result.

##### -> Minimal skill relative to a stack
> **Definition**
>
> Let `s` a given code snippet. We call ***minimal skill relative to `s`*** a skill which is mandatory with a minimum level `l` to be able to understand `s`. The set of the minimal skills relative to `s` is noted ***S<sub>k</sub><sup>s</sup>***.


##### -> Minimal skill relative to a code snippet
> **Definition**
>
> Let `s` a given code snippet. We call ***minimal skill relative to `s`*** a skill which is mandatory with a minimum level `l` to be able to understand `s`. 
> 
> The set of the minimal skills relative to `s` is noted ***S<sub>k</sub><sup>s</sup>***.

**Remark**

* A minimal skill is always relative to a given code snippet. For example, if this code snippet is written in JavaScript, the set of minimal skills must include a minimal level of skill in the mastering of JavaScript.

**Examples of minimal skills**

For any code snippet `s`, the set of minimal skills must include the skills relative to the following fields of competences :

* Algorithmic
* General knowledge in programming
* Specific knowledge in the programming language of `s`
* Specific knowledge in the framework used by the application using `s`
* Mastering of an IDE 

**Remark**

Most of the developers are mastering an IDE, which helps them significantly to increase their productivity. For example, a hovering of the mouse on the identifier of a function may display its signature, and a click on it may open the file containing this function and display its implementation. These features helping considerably the developers to understand the code, we must take this knowledge into account.

[<- Top](#mean-developer)
## The mean developer

Our ultimate goal is to measure the cognitive complexity of a code snippet `s`. To be able to do that, we must use the notion of *mean developer*, which is intuitively a developer which has enough programming knowledge to understand `s`, but which is not necessarily an expert in the programming language. We want to know the time needed by a *"classic"* developer to understand `s`.

A client or a manager needs to know what will be *approximately* the time needed by his developers to maintain the code, fix bugs or develop new features. For that, he needs an approximate value, an estimation of this duration for a *mean developer*. With this value, he will be able to estimate the time needed for *his developers*, knowing for example if they are senior or junior developers.

That's why we need to specify what *"mean developer"* exactly means.

What are the criteria to be taken into account ? What should we assume, and what we should not ?

At first, we should assume that the developer has the minimal programming skills to be able to understand the code snippet. We must assume that he has the minimum level of skills allowing him to understand a code snippet of moderate difficulty without being obstructed by a lack of knowledge.


##### -> Mean developer
> **Definition**
>
> Let `D` the set of all developers having an experience in computer programming which is higher than the minimal experience of computer programming. 
> The ***mean developer*** is a theoretical developer `(h, E)` whose set of experiences `E` is calculated by taking the average of the experiences of the elements of `D`.

**Remark**

* The mean developer has ***mean skills***, which may be calculated by taking the average of the skills of all the elements of `D`.


##### -> Mean developer relative to a stack
> **Definition**
>
> Let `s` a stack, and `D` the set of all developers having an experience in `s` which is higher than the minimal experience of `s`.
> The ***mean developer relative to the stack*** `s` is a theoretical developer `(h, E)` whose set of experiences `E` is calculated by taking the average of the experiences of the elements of `D`.

[<- Top](#mean-developer)
## Understanding speed

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
> In other words, ***S<sub>d</sub>(s) = C<sub>c</sub>(s) / t***, where `t` is the time needed by `d` to understand `s`.

> **Proposition**
>
> The understanding speed of the mean developer is always equal to 1.
 
**Demonstration**

* The cognitive complexity of a code snippet `s` is, by definition, the time needed by the mean developer to understand `s`. If we divide this number by the time that the same mean developer needs to understand `s`, the result of the division will always equal to one.

**Remark**

* If the understanding speed of a code snippet `s` by a developer `d` is equal to 2, `d` understands `s` two times faster than average. 
* If the understanding speed of a code snippet `s` by a developer `d` is equal to 0.5, `d` understands `s` two times slower than average. 

##### -> Expertise level
> **Definition**
>
> The ***expertise level*** of a developer `d` for a stack `s` is the average understanding speed for all the code snippets written with the stack `s`.

**Example**

* If the developer `d` has an expertise level of 2 in TypeScript, he understands, on average, a TypeScript code snippet two times faster than the mean developer.





***Work in progress...***
