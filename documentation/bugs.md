# Bugs

If we are so interested in the concept of cognitive complexity, it's because of its correlation with the software maintainability. A software is easier to maintain if the bugs are easy to fix than if they are difficult to find and to resolve.

Bugs may be caused by the program or by the system itself (hardware, connections, etc.). When we will use the word *bug*, it will be supposed that the problem is caused by the program, not by the hardware or something else.

## Definition of a bug

> **Definition**
>
> A program has a ***bug*** when the [behavior of the system](systems.md) does not respect the [specs](code-snippets-tmp.md#features) asked by the [prime contractor](code-snippets-tmp.md#features).

**Remark**

Assuming that no one prime contractor will ask to develop a feature which will make crash the app, we will suppose that any program which may crash in a real execution has a bug.

**Example**

Assume that the prime contractor asked to display the price of some articles on a web page. Assume now that a lead developer, as intermediate contractor, asks a developer to code a function which will return the price of a given article : 

Here is his code snippet: 
```ts
// Code snippet s
function getPrice(article: Article): number {
	return article.price;
}
```

If it is absolutely sure that the parameter `article` will never be undefined, *and* that the property `price` corresponds to the value expected by the client, there is no bug. If the parameter `article` may be undefined, there is a bug, because the app will crash when `article` will be undefined.

**Remark**

This example clearly demonstrates that we can't say that a code snippet has a bug in absolute terms, without specifying the specs expected by the prime contractor. 

> **Definition**
>
> A ***bug fix*** is a [modification](understanding.md#refactoring) which transforms a program `p` having some bug in a program `p'` without bug which respects the specs specified by the prime contractor.


[Top](#bugs)
## Causes of bugs

The causes of bugs are multiple, and the "wrongdoer" may not be the developer... Let's try to clarify it :

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

Then, the developer must understand *why* the behavior of the system is not correct. We can mention two ways of debugging

#### Reverse debugging

Assume that a client ask a developer to debug its Angular application, which should display the pre-tax price of some articles, but which displays the price including the VAT. What will do the developer ?

* Find and analyze the HTML component

The developer knows the *consequence* of the bug: the displayed price is wrong. He will try to find its *cause*. His first step is to find the HTML component displaying the price. The *cause* of the bug is relative to this HTML file. Now, he needs to find in the HTML file the method which is called to display the price. This method is usually located in the TypeScript component relative to the HTML file. Assume that this function is called `displayPrice()`.

* Find and analyze the TypeScript component

The method `displayPrice()` is probably the *cause* of the wrong value displayed by the HTML file. Its *consequence* is the wrong behavior of the HTML file. Let's look at its implementation:

```ts
@Component(...)
export class ArticlesComponent {
	
	price: number;
	
	// ....
    
    constructor(articlesService: ArticlesService) {
    	
    }
    
	displayPrice(article: Article): number {
		this.price = article.price;
	}
	
}
```

The implementation of `displayPrice()` seems to be correct, it is not the root cause of the bug. The developer must continue to search by reverse order, from the consequences to the causes.

* Find and analyze the TypeScript service

```ts
@Injectable()
export class ArticlesService {

	getArticleUrl: string = 'someUrl';
	
	constructor(private http: HttpClient) { }
	
	getArticle(idArticle: number): Article {
		const url = `${this.getArticleUrl}?id=${idArticle}`;
		return this.http.get(url);
    }
}
```

-----
// TODO: clean

-----

### Bug resolution

Assume that the name of the function of a code snippet `s` was not correctly defined and that we try to use it in another code snippet `t`:

```ts
// Code snippet s
function someFunction(a: number): number {
	// Do complex operations and return some number
}

// Code snippet t
function doComplexCalculations(a: number): number {
	const b: number = someFunction(a);
	// Do some long calculations using b
	return b;
}
```
The code snippet `t` is impossible to debug without reading `s`: the *role* of `s` is not understandable in `t`.

So, if you want to debug `t`, you'll read the code of `s`, but in the aim to understand *what* `someFunction` is doing, not *how* `someFunction` runs. The most important for you is the *role* of `s`, not its `significant`. The *role* of `s` will become important for you if and only if the bug is inside `s`.

It is also the justification of the *documentation*: if `someFunction` is correctly documented, you'll not need to understand its implementation :

```ts
// Code snippet s

// Returns the circumference of a circle of radius a
function someFunction(a: number): number {
	// Do complex operations and return some number
}
```

The comments and the names of the identifiers are probably the most important parameters correlating the cognitive complexity with the understanding of the role of the code snippets, but are not the only ones. Moreover, we could discuss of the real efficiency of the documentation in some specific cases: do we really need documentation for very trivial cases, like for the function `multiplyByTwo` ? Or for the getters and the setters ? If not, in which cases should we add some documentation, and what should we write inside ? We could debate hours and hours about it, without having objective and indiscutable results: we would only have different expert opinions. We need scientific experiments, measures and statistics to be able to say one day: "yes, you should write documentation here, because it is proven that it will reduce the cognitive complexity".

In conclusion, we just need to remember that the understanding of the *role* of the code is important in the aim to understand *other* code snippets (and debug them easier).

***Work in progress...***
