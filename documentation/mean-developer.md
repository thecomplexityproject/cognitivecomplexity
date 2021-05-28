[<-](README.md)
# Mean developer

## Table of contents

* [Introduction](#introduction)
* [Skills](#skills)
  * [Competence](#--competence)
  * [Skill](#--skill)
  * [Skills related to a code snippet](#--skills-related-to-a-code-snippet)
  * [Minimal skill relative to a competence](#--minimal-skill-relative-to-a-competence)
  * [Minimal skill relative to a code snippet](#--minimal-skill-relative-to-a-code-snippet)
* [Developers](#developers)
    * [Human factor](#--human-factor)
    * [Experience](#--experience)
    * [Developer](#--developer)
    * [Minimal experience](#--minimal-experience)
* [The mean developer](#the-mean-developer)
    * [Mean developer](#--mean-developer)
    * [Mean developer relative to a competence](#--mean-developer-relative-to-a-competence)
* [The understanding speed](#the-understanding-speed)
    * [Time of understanding](#--time-of-understanding)
    * [Understanding speed](#--understanding-speed)
    * [Expertise level](#--expertise-level)

[<- Top](#mean-developer)
## Introduction

The definition of the [cognitive complexity](cognitive-complexity.md) uses the term *"mean developer"*. We need to accurate what is exactly a *"mean developer"* to be able to calculate objectively the cognitive complexity of a given code snippet. In other words, we need to precise what are the characteristics of a developer which are correlated to the notion of cognitive complexity.

[<- Top](#mean-developer)
## Skills

##### -> Competence
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
> We call ***skill*** a technical aptitude that can be acquired by a human being in the aim to master a competence. If this competence is called `c`, we say that it is a ***skill related to `c`***.
> 
> A skill may be *quantified*, *measured* or *estimated*. This quantification, measure or estimation is called a ***level of skill***. 

**Remark**

* Thereafter, the word *skill* will always imply that we talk about a *programming skill*. We note ***S<sub>k</sub>*** the set of all the possible programming skills.

##### -> Skills related to a code snippet
> **Definition**
>
> The ***skills related to a code snippet*** `s` are the skills which are mandatory to understand `s`, in the context of the program containing `s`.
>
> More generally, the ***skills related to a set of code snippets `S`*** are the set of skills which are mandatory to understand each element of `S`. Same definition for the skills related to a project, product or program.

**Example**

* If a webapp `w` is developed with the stack MEAN (MongoDB, Express, Angular, NodeJs), the skills related to `w` are the technical aptitudes related to the mastering of MongoDB, Express, Angular and NodeJs.
* When some parts of a program `p` may be completely decoupled, a developer may master only some parts of the stack of `p` to understand a code snippet `s` of `p`. It is true for webapps: the front-end developer does not need to master MongoDB or NodeJs, for example. If `s` is a code snippet located in the frontend, the skills related to `s` are TypeScript, HTML, CSS and Angular.

##### -> Minimal skill relative to a competence
> **Definition**
>
> We call ***minimal skill relative to a competence `c`*** a skill which is mandatory with a minimum level `l` to be able to acquire a basic knowledge of `c`.

**Remarks**

* The word *"basic"* is voluntarily ambiguous. For each competence `c`, it is necessary to specify what is its *"basic knowledge"*. Of course, this ambiguity affects the decision to rank a person in the set of the human beings having a minimum skill related to `c`. However, if our goal is only to avoid the distorsions caused by the complete lack of knowledge in a given field of competence, the choice of the elements defining the basic knowledge of `c` should be easy to do, and its contours should have a minor impact on the calculations.

##### -> Minimal skill relative to a code snippet
> **Definition**
>
> We call ***minimal skill relative to a code snippet `s`*** a skill which is mandatory with a minimum level `l` to be able to understand `s`.
>
> The set of the minimal skills relative to `s` is noted ***K<sub>s</sub><sup>l</sup>***.

**Example**

* If `s` is written in JavaScript, the set of minimal skills must include a minimal level of skill in the mastering of this language.

**Remark**

* A developer `d` may have the minimal skill relative to the competence "JavaScript" without having the minimal skill related to a specific code snippet `s` written in JavaScript. For example, if `s` is very difficult to understand, and if `d` has only the minimal skill in JavaScript, he may not understand `s`. It is normal, and this case should be taken into account in the calculations.

**Remark**

For any code snippet `s`, the set of minimal skills must include the skills relative to the following competences :

* Algorithmic
* General knowledge in programming
* Specific knowledge in the programming language of `s`
* Specific knowledge in the framework used by the application using `s`
* Mastering of an IDE

**Remark**

* Most of the developers are mastering an IDE, which helps them significantly to increase their productivity. For example, a hovering of the mouse on the identifier of a function may display its signature, and a click on it may open the file containing this function and display its implementation. These features helping considerably the developers to understand the code, we must take this knowledge into account.


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
> We call ***experience*** a triplet `(k, t, p)`, where `k` is a skill, and `t` the time spent by a human being to acquire or improve `k` during a period `p`.

**Remark**

* The experience is a human factor. However, it is not the only human factor affecting the level of skills of a human being: two persons with the same recent experience may have different levels of skills.
* `t` and `p` are durations, expressed in time units.
* The specification of the period is useful to improve the correlation between the concept of *"experience"* and the levels of skills. It helps to ensure that the person having this experience did not have time to lose its skills.


##### -> Developer
> **Definition**
>
> A ***developer*** is defined by a couple `(h, E)` where `h` represents a human being and `E` his set of experiences.

**Remark**

* For simplicity, we will frequently use the word *experience* in the singular when we will talk about the set of experiences of a developer. 

> **Conjecture**
> 
> To some extent, the skills of a human being are positively correlated with the length of his experiences.

**Demonstration elements**

* By definition, a skill is obtained by acquiring or improving some competence. It is clear that without any experience in a given field of competence, the skills are nonexistent. Consequently, initially at least, the skills are positively correlated with the experience. 
* Then, it is true likely that a longer experience improves the skills of a human being. However, it is probably true only to some extent. A human being may have a very long experience and forget it after some years without practice.


##### -> Minimal experience
> **Definition**
>
> The ***minimal experience*** in a competence `c` is an arbitrary couple of numbers `(t, p)` which represents the recent experience that a human being must have to master the minimal skills related to `c`.


**Remarks**

* This couple `(t, p)` is arbitrary. It is a *"threshold"* which is defined in the aim to avoid the cases which could distort the calculations. For example, if a developer has absolutely no knowledge in TypeScript and JavaScript, he will need an extremely long time to understand any Angular code snippet. This case could drastically distort the calculation of the cognitive complexity of this code snippet. That's why we need to define this threshold, which represents the time that a developer will need to learn the basics of the stack of the code snippet he reads.

**Example**

We could say that the minimal experience in the competence "JavaScript" is :
  - 1 year of computer programming during the last 5 years
  - 1 month of programming in JavaScript during the last 6 months 
    
With this definition of the *minimal experience in JavaScript*, we can be sure that a developer having this minimal experience will not need days or weeks to understand a JavaScript code snippet of medium difficulty. This threshold will help us to make average calculations avoiding extreme cases which could distort the result.

[<- Top](#mean-developer)
## The mean developer

Our ultimate goal is to measure the cognitive complexity of a code snippet `s`. To be able to do that, we must use the notion of *mean developer*, which is intuitively a developer which has enough programming knowledge to understand `s`, but which is not necessarily an expert in the programming language. We want to know the time needed by a *"classic"* developer to understand `s`.

A client or a manager needs to know what will be *approximately* the time needed by his developers to maintain the code, fix bugs or develop new features. For that, he needs an approximate value, which will help him to estimate the time needed for *his developers*. If they are senior, he will know that they probably need less time than the mean developer, but more time if they are junior developers.

That's why we need to specify what *"mean developer"* exactly means. What are the criteria to be taken into account ? What should we assume, and what we should not ?

At first, we should assume that the developer has the minimal programming skills to be able to understand a code snippet of moderate difficulty without being obstructed by a lack of knowledge.


##### -> Mean developer
> **Definition**
>
> Let `D` the set of all developers having an experience in computer programming which is higher than the minimal experience of computer programming. 
> 
> The ***mean developer*** is a theoretical developer `(h, E)` whose set of experiences `E` is calculated by taking the average of the experiences of the elements of `D`.

**Remark**

* The mean developer has also ***mean skills***, which may be calculated by taking the average of the skills of all the elements of `D`.


##### -> Mean developer relative to a competence
> **Definition**
>
> Let `c` a competence, and `D` the set of all developers having an experience in `c` higher or equal to the minimal experience in `c`.
> 
> The ***mean developer relative to the competence*** `c` is a theoretical developer `(h, E)` whose set of experiences `E` is calculated by taking the average of the experiences of the elements of `D`.

[<- Top](#mean-developer)
## The understanding speed

##### -> Time of understanding
> **Definition**
>
> Let `d` a developer and `s` a code snippet.
> The ***time of understanding*** of `s` by `d` is the time needed by `d` to understand `s`.


##### -> Understanding speed
> **Definition**
>
> The ***understanding speed*** by a given developer `d` of a given code snippet `s` is equal to the cognitive complexity of `s` divided by the time needed by `d` to [understand](understanding.md#--understanding-of-code-snippets) it. We note it ***S<sub>d</sub>(s)***
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
> The ***expertise level*** of a developer `d` for a competence `c` is the average understanding speed for all the code snippets written with the competence `c`.

**Example**

* If the developer `d` has an expertise level 2 in TypeScript, he understands, on average, a TypeScript code snippet two times faster than the mean developer.





***Work in progress...***
