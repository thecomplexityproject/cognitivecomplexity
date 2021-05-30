[<-](README.md)
# Chain of responsibilities

## Table of contents

* [Feature, product, task](#feature-product-task)
  * [Feature](#--feature)
  * [Product](#--product)
  * [Task](#--task)
* [Prime contractor, stakeholders, specs and chain of responsibilities](#prime-contractor-stakeholders-specs-and-chain-of-responsibilities)
  * [Prime contractor](#--prime-contractor)
  * [Stakeholders](#--stakeholder)
  * [Specs](#--specs)
  * [Immediate superior, subordinates](#--immediate-superior-subordinates)
  * [Chain of responsibilities](#--chain-of-responsibilities)
  * [Job](#--job)

[<- Top](#chain-of-responsibilities)
## Feature, product, task


##### -> Feature
> **Definition**
>
> A ***feature*** is a set of functionalities.

##### -> Product
> **Definition**
>
> A ***product*** is a set of features accessible to a human being or to a machine. This human being or machine is called a ***user***.

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

##### -> Job
> **Definition**
> 
> The ***job of a stakeholder*** is to provide something respecting the specs transmitted to him by his superior.

**Remark**

A stakeholder has two responsibilities:
* Check if the work produced by its subordinates corresponds to the tasks he assigned to them.
* Produce himself an additional work which will provide, with the help of the works of his subordinates, a product respecting the specs of the tasks assigned to him. 


***Work in progress...***
