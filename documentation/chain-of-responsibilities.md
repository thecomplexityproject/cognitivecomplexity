[<-](README.md)
# Chain of responsibilities

## Table of contents

* [Feature, product, task](#feature-and-product)
  * [Feature](#--feature)
  * [Product](#--product)
* [Prime contractor, stakeholders, specs and chain of responsibilities](#prime-contractor-stakeholders-specs-and-chain-of-responsibilities)
  * [Prime contractor](#--prime-contractor)
  * [Stakeholders](#--stakeholder)
  * [Task](#--task)
  * [Specs](#--specs)
  * [Immediate superior, subordinates](#--immediate-superior-subordinates)
  * [Chain of responsibilities](#--chain-of-responsibilities)
  * [Job](#--job)

[<- Top](#chain-of-responsibilities)
## Feature and product


##### -> Feature
> **Definition**
>
> A ***feature*** is a set of functionalities accessible to a human being or to a machine. This human being or machine is called a ***user***.

##### -> Product
> **Definition**
>
> A ***product*** is a set of features.


[<- Top](#chain-of-responsibilities)
## Prime contractor, stakeholders, specs and chain of responsibilities

##### -> Stakeholder
> **Definition**
>
> A ***stakeholder*** is a human being which will participate actively in the concrete realisation of the product.

**Remark**

* A prime contractor is a stakeholder.
* A stakeholder may be in charge of one or multiple tasks, features, or even the final product itself.

##### -> Superior, subordinates
> **Definition**
>
> When a stakeholder has the legitimacy to give orders to another one, the first stakeholder is called the ***superior*** of the second stakeholder, which is one of his ***subordinates***.

**Remark**

* We assume that each stakeholder has only one immediate superior.

##### -> Chain of responsibilities, prime contractor
> **Definition**
>
> Let `S` a set of stakeholders. We say that `S` is a ***chain of responsibilities*** if:
> * There is a single element of `S` which has no superior in `S`. This element is called the ***prime contractor***.
> * There is a single element of `S` which has no subordinate in `S`, and which is not the top of the chain.
> * All the other elements of `S` have a single superior and a single subordinate in `S`.
>
> The elements of `S` are called the ***links*** of the chain.

##### -> Flow chart
> **Definition**
>
> A ***flow chart*** is a set of chain of responsibilities having the same top of the chain.


##### -> Role of a functionality
> **Definition**
>
> Let `f` a functionality imagined by a stakeholder `s`. 
> 
> The ***role of the functionality `f`*** is the behavior of the system expected by `s` which corresponds to this functionality .

##### -> Task
> **Definition**
>
> Let `f` a functionality imagined by a stakeholder `s`.
> 
> A ***task*** is an order given by `s` to one of his subordinates in the aim to provide a behavior of the system corresponding to the role of `f`.


##### -> Specs
> **Definition**
>
> Let `t` a task given by a stakeholder `s` to his subordinate `s'`. Let `f`the functionality corresponding to `t`.
> 
> The ***specs*** of `f` are the oral and written instructions specified by `s` to `s'` in the aim to perform this task.


##### -> Job
> **Definition**
> 
> The ***job of a stakeholder*** is to provide to his superior the results of the tasks corresponding to the specs specified by his superior.

**Remarks**

A stakeholder has two responsibilities:
* Check if the work produced by its subordinates corresponds to the tasks he assigned to them.
* Produce himself an additional work which will provide, with the help of the works of his subordinates, a product respecting the specs of the tasks assigned to him. 

##### -> Implementation of a functionality
> **Definition**
>
> Let `t` a task given to a developer `d`. The job of `d` is to ***implement the functionality*** corresponding to `t`, *i.e.* to write the code snippets providing the behavior of the system corresponding to the specs given by his superior. 

**Remark**

* Each code snippet written by `d` will contain declared references, and each of them will have a *role* given by `d`. See the definition of the [role of a reference](code-snippets-tmp.md#--role-of-references).

***Work in progress...***
