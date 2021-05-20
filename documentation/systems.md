
# Systems

## Features, products and tasks


> **Definition**
>
> A ***feature*** is a set of functionalities imagined by a natural person to provide to the users.
>
> The ***final product*** is the set of all the features to provide to the users.
>
> A ***task*** is a set of functionalities imagined by a natural person in the aim to provide a given behavior to the system in specific situations. In other words, a task may be a subset of a feature, or a subset of another task.

**Remark**

* A feature, a product or a task is something which is *imagined* by a natural person: it is not something concrete which exists in the real world.
* A feature is a task itself.

> **Definition**
>
> The ***prime contractor*** is the natural person which imagines the final product.
>
> A ***stakeholder*** is a natural person which will participate actively in the concrete realisation of the product.

**Remark**

* A prime contractor is a stakeholder.
* A stakeholder may be in charge of one or multiple tasks, features, or even the final product itself.

> **Definition**
>
> The ***specs*** of a given task are the oral and written instruction specified by the author of the task, in the aim to provide the set of functionalities defining this task.

**Remark**

* Thereafter, we will always suppose that the specs were written, even if the author of the task is assigning it to himself. Consequently, a spec is formulated in the real world. It is something concrete which is the only source of information available for the stakeholder which will execute the task.

## Prime contractor, stakeholders, specs and chain of responsibilities

> **Definition**
> 
> When the specs are transmitted from a stakeholder to another one, the first stakeholder is called the ***immediate superior*** of the second stakeholder, which is one of his ***subordinates***.

**Remark**

* We assume that each stakeholder has only one immediate superior.

> **Definition**
> 
> Let `S` a set of stakeholders. We say that `S` is a ***chain of responsibilities*** if:
> * There is a single element of `S` which has no superior in `S`. This element is called the ***top of the chain***.
> * There is a single element of `S` which has no subordinate in `S`, and which is not the top of the chain. This element is called the ***bottom of the chain***.
> * All the other elements of `S` have a single superior and a single subordinate in `S`. They are called the ***intermediates of the chain***.
> 
> The elements of `S` are called the ***links*** of the chain.

> **Definition**
> 
> The ***job of a stakeholder*** is to provide a ***product*** respecting the specs transmitted to him by his superior.

**Remark**

A stakeholder has two responsibilities:
* Check if the work produced by its subordinates corresponds to the tasks he assigned to them.
* Produce himself an additional work which will provide, with the help of the works of his subordinates, a product respecting the specs of the tasks assigned to him. 

## Systems

> **Definition**
>
> We call ***system*** the triplet (H, S, D) corresponding to a functional set, where H is a hardware, S is a software, and D some data.
> 
> The ***role of a system*** is to provide to the users the features corresponding to an expected product.


> **Definition [<sup>w</sup>](https://en.wikipedia.org/wiki/Information_system)**
>
> The term ***hardware*** refers to machinery and equipment. In a modern information system, this category includes the computer itself and all of its support equipment. The support equipment includes input and output devices, storage devices and communications devices.

> **Definition [<sup>w</sup>](https://en.wikipedia.org/wiki/Information_system)**
>
> The term ***software*** refers to computer programs defined as the machine-readable instructions that direct the circuitry within the hardware parts of the system to function in ways that produce useful information from data.
>
> Thereafter, we will simply call ***program*** the set of machine-readable instructions of a given system. In other words, the program is the set of the modules of the software.

**Remark**

In terms of functionalities, we can also say that the aim of a software is to provide a set of [features](code-snippets-tmp.md#features) to the users. 

> **Definition [<sup>w</sup>](https://en.wikipedia.org/wiki/Information_system)**
>
> ***data*** are facts that are used by systems to produce useful information. In modern information systems, data are generally stored in machine-readable form on disk until the computer needs them.

By nature, a system evolves over time as a result of the current processes running on it, and because of the eventual inputs received from out of the system.

> **Definition**
>
> A ***process*** is a triplet `(S, l, p)` where `l` is the instruction currently executed by a processor `p` in a given system `S`.


> **Definition**
>
> The ***state of the system*** `S` is the couple `(D, P)` where `D` represents the data of the system and `P` the set of processes running at a time `t`.


> **Definition**
>
> The ***behavior of a system*** is the evolution of its state during the execution of a given process.

**Remarks**

* *system* and *hardware* are in the *world of measurability*, *i.e.* are referring to objects located in the real world.
* *software*, *data*, *process*, *state of the system*, *behavior of a system* are in the *world of the computability*, *i.e.* are referring to theoretical objects.

***Work in progress...***
