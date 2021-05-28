[<-](README.md)
# Systems and stakeholders

## Table of contents

* [Feature, final product, task](#feature-final-product-task)
  * [Feature](#--feature)
  * [Final product](#--final-product)
  * [Task](#--task)
* [Prime contractor, stakeholders, specs and chain of responsibilities](#prime-contractor-stakeholders-specs-and-chain-of-responsibilities)
  * [Prime contractor](#--prime-contractor)
  * [Stakeholders](#--stakeholder)
  * [Specs](#--specs)
  * [Immediate superior, subordinates](#--immediate-superior-subordinates)
  * [Chain of responsibilities](#--chain-of-responsibilities)
  * [Job, product](#--job-product)
* [Systems](#systems)
  * [System, role of a system](#--system-role-of-a-system)
  * [Hardware](#--hardware)
  * [Software, program](#--software-program)
  * [Data](#--data)
  * [Process](#--process)
  * [State of the system](#--state-of-the-system)
  * [Behavior of the system](#--behavior-of-the-system)

[<- Top](#systems-and-stakeholders)
## Feature, final product, task


##### -> Feature
> **Definition**
>
> A ***feature*** is a set of functionalities imagined by a natural person to provide to the users.

##### -> Final product
> **Definition**
>
> The ***final product*** is the set of all the features to provide to the users.

##### -> Task
> **Definition**
>
> A ***task*** is a set of functionalities imagined by a natural person in the aim to provide a given behavior to the system in specific situations. In other words, a task may be a subset of a feature, or a subset of another task.

**Remark**

* A feature, a product or a task is something which is *imagined* by a natural person: it is not something concrete which exists in the real world.
* A feature is a task itself.

## Prime contractor, stakeholders, specs and chain of responsibilities

##### -> Prime contractor
> **Definition**
>
> The ***prime contractor*** is the natural person which imagines the final product.

##### -> Stakeholder
> **Definition**
>
> A ***stakeholder*** is a natural person which will participate actively in the concrete realisation of the product.

**Remark**

* A prime contractor is a stakeholder.
* A stakeholder may be in charge of one or multiple tasks, features, or even the final product itself.

##### -> Specs
> **Definition**
>
> The ***specs*** of a given task are the oral and written instruction specified by the author of the task, in the aim to provide the set of functionalities defining this task.

**Remark**

* Thereafter, we will always suppose that the specs were written, even if the author of the task is assigning it to himself. Consequently, a spec is formulated in the real world. It is something concrete which is the only source of information available for the stakeholder which will execute the task.


##### -> Immediate superior, subordinates
> **Definition**
> 
> When the specs are transmitted from a stakeholder to another one, the first stakeholder is called the ***immediate superior*** of the second stakeholder, which is one of his ***subordinates***.

**Remark**

* We assume that each stakeholder has only one immediate superior.

##### -> Chain of responsibilities
> **Definition**
> 
> Let `S` a set of stakeholders. We say that `S` is a ***chain of responsibilities*** if:
> * There is a single element of `S` which has no superior in `S`. This element is called the ***top of the chain***.
> * There is a single element of `S` which has no subordinate in `S`, and which is not the top of the chain. This element is called the ***bottom of the chain***.
> * All the other elements of `S` have a single superior and a single subordinate in `S`. They are called the ***intermediates of the chain***.
> 
> The elements of `S` are called the ***links*** of the chain.

##### -> Job, product
> **Definition**
> 
> The ***job of a stakeholder*** is to provide a ***product*** respecting the specs transmitted to him by his superior.

**Remark**

A stakeholder has two responsibilities:
* Check if the work produced by its subordinates corresponds to the tasks he assigned to them.
* Produce himself an additional work which will provide, with the help of the works of his subordinates, a product respecting the specs of the tasks assigned to him. 

[<- Top](#systems-and-stakeholders)
## Systems


##### -> Hardware
> **Definition**
>
> The term ***hardware*** refers to machinery and equipment. It includes the computer itself and all of its support equipment. The support equipment includes input and output devices, storage devices and communications devices.

##### -> File
> **Definition**
>
> A ***file*** is a document containing machine-readable instructions, recorded in some part of a hardware.

**Remark**

Of course, in the real world, a file can't be defined with only these 4 elements, but for our purpose, we only need them.

##### -> Module
> **Definition**
>
> The set of machine-readable instructions of a file is called a ***module***.

##### -> Software
> **Definition**
>
> A ***software*** is a set of files that direct the circuitry within the hardware parts of the system in the aim to provide some features to the users.

##### -> Program
> **Definition**
>
> A ***program*** is the set of modules of a given software.

**Remark**

In terms of functionalities, we can also say that the aim of a software is to provide a set of features to the users. 

##### -> System
> **Definition**
>
> We call ***system*** the triplet (H, S, D) corresponding to a functional set, where H is a hardware, S is a software, and D some data.
>
> The role of a system is to provide to the users the features corresponding to an expected final product.

##### -> Data
> **Definition**
>
> ***data*** are facts that are used by a system to produce useful information. They are generally stored in machine-readable form on disk until the computer needs them.

By nature, a system evolves over time as a result of the current processes running on it, and because of the eventual inputs received from out of the system.

##### -> Process
> **Definition**
>
> A ***process*** of a program `P` is a couple `(l, p)` where `l` is the instruction of `P` currently executed by a processor `p`.

##### -> State of the system
> **Definition**
>
> The ***state of a system*** `S` is the couple `(D, P)` where `D` represents the data of the system and `P` the set of processes running at a time `t`.

##### -> Behavior of the system
> **Definition**
>
> The ***behavior of a system*** is the evolution of its state during the execution of a given process.

**Remarks**

* *system* and *hardware* are in the *world of measurability*, *i.e.* are referring to objects located in the real world.
* *software*, *data*, *process*, *state of the system*, *behavior of a system* are in the *world of the computability*, *i.e.* are referring to theoretical objects.

***Work in progress...***
