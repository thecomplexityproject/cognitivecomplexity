# Bugs

If we are so interested in the concept of cognitive complexity, it's because of its correlation with the software maintainability. A software is easier to maintain if the bugs are easy to fix than if they are difficult to find and to resolve.

Bugs may be caused by the program or by the system itself (hardware, connections, etc.). When we will use the word *bug*, it will be supposed that the problem is caused by the program, not by the hardware or something else.

## Table of contents

* [Definition of a bug](#definition-of-a-bug)
* [Causes of bugs](#causes-of-bugs)
  * [Misunderstanding](#misunderstanding)
  * [Wrong implementation](#wrong-implementation)
  * [Wrong reuse](#wrong-reuse)
* [Debugging process](#debugging-process)
  * [Bug discovering](#bug-discovering)
  * [Bug understanding](#bug-understanding)
* [Bugs and cognitive complexity](#bugs-and-cognitive-complexity)


## Definition of a bug

> **Definition**
>
> A feature or a task ***has a bug*** when the [behavior of the system](systems.md) does not respect its [specs](systems.md#prime-contractor-stakeholders-specs-and-chain-of-responsibilities). 
> 
> A ***bug*** of a feature (or task) is a [state of the system](systems.md) which will cause a behavior not respecting the specs of this feature (or task).

**Remark**

By extension, we say that a *product*, or a *program*, has a bug when one of its features has a bug.

**Remark**

Assuming that no one will ask to develop a feature which will make crash the program, we will suppose that any context-sensitive code snippet which may crash during a real execution has a bug.

**Example**

Assume that a stakeholder writes the following specs, and transmit them to a developer:

* *Implement a function which will return the price of a given article.* 

Here is the code snippet written by the developer: 
```ts
// Code snippet s
function getPrice(article: Article): number {
	return article.price;
}
```

The code snippet `s` respects the specs, thus the developer didn't introduce a new bug.


If it is absolutely sure that the parameter `article` will never be undefined, *and* that the property `price` corresponds to the value expected by the client, there is no bug. If the parameter `article` may be undefined, there is a bug, because the app will crash when `article` will be undefined.

**Remark**

This example clearly demonstrates that we can't say that a code snippet has a bug in absolute terms, without specifying the specs expected by the prime contractor. 


> **Definition**
>
> A reference `r` ***has a bug*** when its [behavior](code-snippets-tmp.md#references) differs from its [role](code-snippets-tmp.md#roles-and-descriptions).
>
> A ***bug*** of a reference `r` is a [state of the system](systems.md) which will cause a behavior of `r` in contradiction with its role.
>
> A context-sensitive code snippet `s` ***has a bug*** when one of the references declared in `s` has a bug.
> 
> A ***bug*** of a context-sensitive code snippet `s` is a [state of the system](systems.md) which will cause a bug for one of the references declared in `s`.


[comment]: <> (> **Definition**)

[comment]: <> (>)

[comment]: <> (> A ***bug fix*** is a [modification]&#40;understanding.md#refactoring&#41; which transforms a program `p` having some bug in a program `p'` respecting the specs specified by the prime contractor.)


[Top](#bugs)
## Sources of bugs

The causes of bugs are multiple, and the "wrongdoer" may not be the developer... Let's try to clarify it :

> **Definition**
>
> A reference is a ***source of bugs*** if its description is incorrect or insufficient to be able to guess its precise behavior.

### Misunderstanding

The main cause of bugs is probably a misunderstanding between two consecutive links of the [chain of responsibilities](code-snippets-tmp.md#features).

> **Definition**
> 
> A ***misunderstanding*** between two consecutive element of a chain of responsibilities happens when there is a difference between what thinks the superior element and what the inferior element thinks that his superior thinks.

**Example 1**

Assume that a client asks a developer to code a function which will return the price of a given article, in the aim to display its price on a web page. If it was clear in the mind of the client that the displayed price must be the pre-tax price, and if the developer thought that it should be the price including the VAT, there is a misunderstanding between the client and the developer.

If it was not explicitly specified that the price must be without VAT, *it is not a bug*, because the developer respected the specs explicitly given by the client. It is a lack of specs. In this case, the client is the wrongdoer. If it was explicitly specified, it is a bug, and the developer is the wrongdoer.

**Example 2**

Assume now that we add a link to the chain of responsibilities: a lead developer. If the client explicitly specified that the price must be without VAT, and if the lead developer didn't give this information to the developer, there will be a bug, but the wrondoer will be the lead developer.

### Wrong implementation

> **Definition**
>
> A program has a ***wrong implementation*** when there is no misunderstanding, and when the behavior of the system does not respect the specs of the different features asked by the prime contractor.

**Example**

In the example above, assume that the client wanted to display the pre-tax price, and there was no misunderstanding in the chain of responsibilities. If the displayed value is not the pre-tax price of the article, there is a wrong implementation. 

**Remark**

In case of wrong implementation, the wrongdoer may not be the developer. For example, an architect may ask developers to implement some functionalities. All the code snippets may respect the specs asked by the architect, but the combination of all these code snippets may not provide the behavior expected by the client. In this case, the wrongdoer is the architect.

### Wrong reuse

> **Definition**
> 
> A ***reuse*** of a program, a feature or a code snippet `s`, is the usage of `s` in a context defined by specs which are different from the original specs. 

**Example**

Assume that a client asked to develop a web page for professionals displaying the pre-tax of some articles. Assume that there is no bug, and that the code snippet below returns the correct value :

```ts
// Code snippet s
function getPrice(article: Article): number {
	return article.price;
}
```

Now, assume that the client wants a second page for individuals displaying the articles including the VAT. If the implementation of this new feature uses `s`, it is a reuse of `s`. 

If it is a new developer which is implementing this new feature, he will maybe not understand that the function `getPrice()` will return the *pre-tax* price. In this case, there will be an implementation bug. This bug happens because the new developer don't [understand](understanding.md#understanding-of-valid-code-snippets) the role of `s`.


[Top](#bugs)
## Debugging process

### Bug discovering

A bug may be detected by two kinds of actors:
* The prime contractor or the users, which may detect that for a given feature, the behavior of the system is not as expected.
* Other links of the chain of responsibilities, which may detect that the behavior of the system is not respecting the specs specified by one of its superiors.

Of course, the second case is preferable to the first.

### Bug understanding

A bug is discovered by someone which is able to understand the specs specified by the prime contractor or by one of its superiors. When this bug is discovered, he may fix the bug himself (if he is a developer), or ask one of his subordinates to do it. To be able to do that, the developer must find the set of code snippets causing this bug. Please note that for now, its only information is provided by the behavior of the system, not by the code itself.

Then, the developer must understand *why* the behavior of the system is not correct.

**Example**

Assume that a client ask a developer `d` to debug its Angular application, which should display the price including VAT of some articles, but which displays the pre-tax prices. This application was developed 6 months ago by a frontend developer `f` and a backend developer `b`, which had the same superior in the chain of responsibilities: a lead developer `l`. What will do our developer `d` to find the bug ?

* Find and analyze the HTML component

His first step is to find the HTML component displaying the price. After that, he needs to find in the HTML file the property name which is displaying the price. This property is located in the TypeScript component relative to the HTML file. Assume that this property is called `price`.

* Find and analyze the TypeScript component

The property `price` is provided by the method `displayPrice()`, which is calling a service returning an article with a given `idArticle`.

```ts
@Component(...)
export class ArticlesComponent {
	
	price: number;
	
	// ....
    
    constructor(articlesService: ArticlesService) {
    	
    }
    
	displayPrice(idArticle: number): void {
		this.price = articlesService.getArticle(idArticle).subscribe(article => this.price = article.price);
	}
	
}
```

The implementation of `displayPrice()` seems to be correct, it is not the root cause of the bug.

* Find and analyze the TypeScript service

The service `getArticle()` simply calls an `http` GET request and returns its response:

```ts
@Injectable()
export class ArticlesService {

	getArticleUrl: string = 'someUrl';
	
	constructor(private http: HttpClient) { }
	
	getArticle(idArticle: number): Observable<Article> {
		const url = `${this.getArticleUrl}?id=${idArticle}`;
		const article = this.http.get(url) as Article; // Here, the `as Article`is a bad practice. We use it to simplify the reasoning.
        return article; 
    }
}
```

Assume that the developer adds a `console.log()` before the `return` line, and that the displayed value is the price including the VAT instead of the pre-tax price. Should he deduce that the method `getArticle()` has a wrong implementation ? That's not so sure.

The problem is that `d` can't understand two things: the `role` of the property `price` of the data returned by the `http` request, and the role of the method `getPrice()`. The role of the property `price` was defined by the backend developer `b`, and the role of `getPrice()` was defined by the frontend developer `f`. Where is the mistake, and who is the wrongdoer ?

  * First case: the lead developer `l` specified that the property `price` returned by the `http` request must be the pre-tax price

    In this case, `f` is the wrongdoer. He should add the VAT to the value of the property `price`.

  * Second case: the lead developer `l` specified that the property `price` returned by the `http` request must be the price including the VAT

    In this case, `b` is the wrongdoer. He should add the VAT to the value of the property `price`.

  * Third case: the lead developer `l` didn't specify anything about the property `price`.

    In this case, `l` is maybe the wrongdoer, because he perhaps should specify the role of `price`. We could also think that `f` and `b` are the wrongdoers, because they should discuss together before the creation of the `http` request.

  * Fourth case: `l`, `f` and `b` are not the wrongdoers.

    It is possible that all was clear for `l`, `f` and `b`, and that their implementation of the task was correct. The wrongdoer is perhaps a fourth developer, which used a `POST` request which sent in the database a pre-tax price instead of a price including the VAT.

So, what should do our developer `d` to fix the bug ?

The first three cases are simple to fix: `d` only needs to modify one line in the backend or in the frontend to include the VAT.

The fourth case is the most difficult to solve, because it means that there are in the database some articles which have a price with VAT and others not. It will be extremely long to separate the articles with a price including the VAT from the others, and it will be impossible to do it without the help of the client, which is the only one who knows what is the correct price of each article. The cost of this fix will be very high.

This example is interesting, because it shows that a same apparent bug may take 10 minutes to fix it, or may take 3 weeks... That's why it is so difficult to agree in advance with the client of the price for the maintenance of its code. 

[-> Top](#bugs)
## Bugs and cognitive complexity

The previous example shows that the core of the cause of the bug was the lack of precision of the *role* of the property `price`. Because of it, the developers using this property may not *understand* its role, and thus create a bug. If this property had been called `preTaxPrice` or `priceWithVat`, it is highly probable that this bug never happened. 

It is a problem of cognitive complexity: a developer will understand easier the role of a property called `preTaxPrice` or `priceWithVat` than a property called `price`. Specifically, it is a problem of *spread* of cognitive complexity: something which was clear in the mind of the first developers was not clear at all for the others. That's why, when we measure the cognitive complexity of a code snippet, we must remember that in the [definition of the cognitive complexity](cognitive-complexity.md), the word *mean developer* is relative to an *external* developer, someone which reads the code snippet without knowing the *roles* of its *imported references*. 


***Work in progress...***
