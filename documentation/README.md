# Documentation

## Thematics

This documentation is organized by thematics :

* The definition of Cognitive Complexity
* The set of code snippets
* The notion of *understanding*
* The bugs
* Simplification technics
* The mean developer
* The systems
* The experimental protocols

You will find below a [glossary](#glossary) with the definitions of all the concepts used in this project.

## Propositions and conjectures

Some results ensue directly from the definitions of the different concepts described in this documentation and don't need experiments in the real world. We call them ***propositions***.

Other results are probably true, but must be calculated or measured in the real world. These results need the help of experimental studies to demonstrate their validity. We call them ***conjectures***.

## Table of contents

### [Cognitive Complexity](cognitive-complexity.md)

* [Definitions](cognitive-complexity.md#definitions)
  * [Cognitive complexity](cognitive-complexity.md#--cognitive-complexity)
  * [Cognitive complexity metric](cognitive-complexity.md#--cognitive-complexity-metric)
  * [Relation between cognitive complexity and debugging](cognitive-complexity.md#--relation-between-cognitive-complexity-and-debugging)
  * [Minimal cognitive complexity](cognitive-complexity.md#--minimal-cognitive-complexity)
* [Refactoring](cognitive-complexity.md#refactoring)
  * [Modification](cognitive-complexity.md#--modification)
  * [Refactor](cognitive-complexity.md#--refactor)
  * [Simplification](cognitive-complexity.md#--simplification)

### [Code snippets](code-snippets-tmp.md)

* [Programming language](code-snippets-tmp.md#programming-language)
  * [Texts and characters](code-snippets-tmp.md#--texts-and-characters)
  * [Programming language, alphabet, word](code-snippets-tmp.md#--programming-language-alphabet-word)
  * [Formal language, formal grammar](code-snippets-tmp.md#--formal-language-formal-grammar)
  * [Syntax](code-snippets-tmp.md#--syntax)
  * [Separator](code-snippets-tmp.md#--separator)
  * [String](code-snippets-tmp.md#--string)
  * [File](code-snippets-tmp.md#--file)
* [The set of code snippets](code-snippets-tmp.md#the-set-of-code-snippets)
  * [Code snippet (large definition)](code-snippets-tmp.md#--code-snippet-large-definition)
  * [Code snippet (strict definition), context-sensitive valid code snippet, context-free code snippet, validatable code snippet](code-snippets-tmp.md#--code-snippet-strict-definition-context-sensitive-valid-code-snippet-context-free-code-snippet-validatable-code-snippet)
  * [Line of code](code-snippets-tmp.md#--line-of-code)
  * [Module](code-snippets-tmp.md#--module)
* [Implementation and behavior](code-snippets-tmp.md#implementation-and-behaviors)
  * [Implementation](code-snippets-tmp.md#--implementation)
  * [Behavior](code-snippets-tmp.md#--behavior)
* [References](code-snippets-tmp.md#references)
  * [Reference, identifier](code-snippets-tmp.md#--reference-identifier)
  * [Description, declaration and implementation of a reference](code-snippets-tmp.md#--description-declaration-and-implementation-of-a-reference)
  * [Exported and imported references](code-snippets-tmp.md#--exported-and-imported-references)
  * [Exposed and hidden references](code-snippets-tmp.md#--exposed-and-hidden-references)
  * [Behavior of a reference](code-snippets-tmp.md#--behavior-of-a-reference)
  * [Stub](code-snippets-tmp.md#--stub)
  * [Mock](code-snippets-tmp.md#--mock)
  * [Deterministic stub](code-snippets-tmp.md#--deterministic-stub)
  * [Deterministic reference](code-snippets-tmp.md#--deterministic-reference)
* [Roles and descriptions](code-snippets-tmp.md#roles-and-descriptions)
  * [Role of references](code-snippets-tmp.md#--role-of-references)
  * [Quality level of descriptions](code-snippets-tmp.md#--quality-level-of-descriptions)
* [Unit tests](code-snippets-tmp.md#unit-tests)
  * [Unit test](code-snippets-tmp.md#--unit-test)
* [Operations on code snippets](code-snippets-tmp.md#operations-on-code-snippets)
  * [Addition](code-snippets-tmp.md#--addition)
  * [Propositions and conjectures](code-snippets-tmp.md#propositions-and-conjectures)
  
### [The notion of *understanding*](understanding.md)

* [Introduction](understanding.md#introduction)
* [Behavior](understanding.md#behavior)
  * [Behavior prediction and understanding](understanding.md#--behavior-prediction-and-understanding)
* [Role](understanding.md#role)
  * [Role understanding of declared or imported references](understanding.md#--role-understanding-of-declared-or-imported-references)
  * [Description understanding, implementation understanding](understanding.md#--description-understanding-implementation-understanding)
  * [Reference understanding](understanding.md#--reference-understanding)
* [Code snippets](understanding.md#code-snippets)
  * [Understanding of code snippets](understanding.md#--reference-understanding)
  
### [The simplification technics](simplification-technics.md)

* [Remove the dead code](simplification-technics.md#remove-the-dead-code)
* [Clarify identifiers](simplification-technics.md#clarify-identifiers)
* [Add comments](simplification-technics.md#add-comments)
* [Typing](simplification-technics.md#typing)
* [Logic extraction](simplification-technics.md#logic-extraction)
* [Remove line-breaks](simplification-technics.md#remove-line-breaks)

### [The bugs](bugs.md)

* [Definitions](bugs.md#definitions)
  * [Bug of a task or feature](bugs.md#--bug-of-a-task-or-feature)
  * [Bug of a reference or code snippet](bugs.md#--bug-of-a-reference-or-code-snippet)
* [Sources of bugs](bugs.md#sources-of-bugs)
  * [Misunderstanding](bugs.md#--misunderstanding)
  * [Wrong implementation](bugs.md#--wrong-implementation)
  * [Wrong reuse](bugs.md#--wrong-reuse)
* [Debugging process](bugs.md#debugging-process)
  * [Bug discovering](bugs.md#bug-discovering)
  * [Bug understanding](bugs.md#bug-understanding)
* [Bugs and cognitive complexity](bugs.md#bugs-and-cognitive-complexity)


### [The mean developer](mean-developer.md)

* [Definition](mean-developer.md#definition)

### [Systems and stakeholders](systems.md)

* [Feature, final product, task](systems.md#feature-final-product-task)
  * [Feature](systems.md#--feature)
  * [Final product](systems.md#--final-product)
  * [Task](systems.md#--task)
* [Prime contractor, stakeholders, specs and chain of responsibilities](systems.md#prime-contractor-stakeholders-specs-and-chain-of-responsibilities)
  * [Prime contractor](systems.md#--prime-contractor)
  * [Stakeholders](systems.md#--stakeholder)
  * [Specs](systems.md#--specs)
  * [Immediate superior, subordinates](systems.md#--immediate-superior-subordinates)
  * [Chain of responsibilities](systems.md#--chain-of-responsibilities)
  * [Job, product](systems.md#--job-product)
* [Systems](systems.md#systems)
  * [System, role of a system](systems.md#--system-role-of-a-system)
  * [Hardware](systems.md#--hardware)
  * [Software, program](systems.md#--software-program)
  * [Data](systems.md#--data)
  * [Process](systems.md#--process)
  * [State of the system](systems.md#--state-of-the-system)
  * [Behavior of the system](systems.md#--behavior-of-the-system)


### [The experimental protocols](experimental-protocols.md)

* [Methodology](experimental-protocols.md#methodology)


## Glossary


* [Addition](code-snippets-tmp.md#--addition) (of two code snippets)
* [Alphabet](code-snippets-tmp.md#--programming-language-alphabet-word)
* [Behavior](code-snippets-tmp.md#--behavior) (of a code snippet)
* [Behavior](code-snippets-tmp.md#--behavior) (of a reference)
* [Behavior](understanding.md#--behavior-prediction-and-understanding) (prediction of)
* [Behavior](understanding.md#--behavior-prediction-and-understanding) (understanding of)
* [Bug](bugs.md#--bug-of-a-reference-or-code-snippet) (of a reference or code snippet)
* [Bug](bugs.md#--bug-of-a-task-or-feature) (of a task or feature)
* [Bug](bugs.md#--misunderstanding) (misunderstanding)
* [Bug](bugs.md#--wrong-implementation) (wrong implementation)
* [Bug](bugs.md#--wrong-reuse) (wrong reuse)
* [Chain of responsibilities](systems.md#--chain-of-responsibilities)
* [Chain of responsibilities](systems.md#--immediate-superior-subordinates) (immediate superior, subordinate)
* [Character](code-snippets-tmp.md#--texts-and-characters)
* [Code snippet](code-snippets-tmp.md#--code-snippet-large-definition) (large definition)
* [Code snippet](code-snippets-tmp.md#--code-snippet-strict-definition-context-sensitive-valid-code-snippet-context-free-code-snippet-validatable-code-snippet) (context-sensitive valid)
* [Code snippet](code-snippets-tmp.md#--code-snippet-strict-definition-context-sensitive-valid-code-snippet-context-free-code-snippet-validatable-code-snippet) (context-free valid)
* [Code snippet](code-snippets-tmp.md#--code-snippet-strict-definition-context-sensitive-valid-code-snippet-context-free-code-snippet-validatable-code-snippet) (strict definition)
* [Code snippet](understanding.md#--reference-understanding) (understanding)
* [Code snippet](code-snippets-tmp.md#--code-snippet-strict-definition-context-sensitive-valid-code-snippet-context-free-code-snippet-validatable-code-snippet) (validatable)
* [Cognitive complexity](cognitive-complexity.md#--cognitive-complexity)
* [Cognitive complexity](cognitive-complexity.md#--cognitive-complexity-metric) (metric)
* [Cognitive complexity](cognitive-complexity.md#--minimal-cognitive-complexity) (minimal)
* [Data](systems.md#--data)
* [Description](code-snippets-tmp.md#--description-declaration-and-implementation-of-a-reference) (description of)
* [Description](code-snippets-tmp.md#--quality-level-of-descriptions) (quality level)
* [Developer](mean-developer.md) (mean)
* [Feature](systems.md#--feature)
* [File](code-snippets-tmp.md#--file)
* [Formal grammar](code-snippets-tmp.md#--formal-language-formal-grammar)
* [Formal language](code-snippets-tmp.md#--formal-language-formal-grammar)
* [Hardware](systems.md#--hardware)
* [Line of code](code-snippets-tmp.md#--line-of-code)
* [Implementation](code-snippets-tmp.md#--implementation) (of a feature)
* [Implementation](code-snippets-tmp.md#--behavior) (of a code snippet)
* [Mock](code-snippets-tmp.md#--mock)
* [Module](code-snippets-tmp.md#--module)
* [Prime contractor](systems.md#--prime-contractor)
* [Process](systems.md#--process)
* [Product](systems.md#--final-product) (final)
* [Product](systems.md#--job-product) (of a stakeholder)
* [Program](systems.md#--software-program)
* [Programming language](code-snippets-tmp.md#--programming-language-alphabet-word)
* [Refactor](cognitive-complexity.md#--refactor)
* [Refactor](cognitive-complexity.md#--modification) (modification)
* [Refactor](cognitive-complexity.md#--simplification) (simplification)
* [Reference](code-snippets-tmp.md#--reference-identifier)
* [Reference](code-snippets-tmp.md#--description-declaration-and-implementation-of-a-reference) (declaration of)
* [Reference](code-snippets-tmp.md#--description-declaration-and-implementation-of-a-reference) (description of)
* [Reference](code-snippets-tmp.md#--deterministic-stub) (deterministic)
* [Reference](code-snippets-tmp.md#--exported-and-imported-references) (exported)
* [Reference](code-snippets-tmp.md#--exposed-and-hidden-references) (exposed)
* [Reference](code-snippets-tmp.md#--exposed-and-hidden-references) (hidden)
* [Reference](code-snippets-tmp.md#--reference-identifier) (identifier of)
* [Reference](code-snippets-tmp.md#--exported-and-imported-references) (imported)
* [Reference](code-snippets-tmp.md#--description-declaration-and-implementation-of-a-reference) (implementation of)
* [Reference](understanding.md#--role-understanding-of-declared-or-imported-references) (role understanding)
* [Role](code-snippets-tmp.md#--role-of-references) (of a reference)
* [Role](systems.md#--system-role-of-a-system) (of a system)
* [Role](code-snippets-tmp.md#--role-of-references) (in the context of a given code snippet)
* [Role](understanding.md#--role-understanding-of-declared-or-imported-references) (understanding)
* [Separator](code-snippets-tmp.md#--separator)
* [Software](systems.md#--software-program)
* [Specs](systems.md#--specs)
* [Stakeholder](systems.md#--stakeholder)
* [Stakeholder](systems.md#--job-product) (job of)
* [String](code-snippets-tmp.md#--string)
* [Stub](code-snippets-tmp.md#--stub)
* [Stub](code-snippets-tmp.md#--deterministic-stub) (deterministic)
* [Syntax](code-snippets-tmp.md#--syntax)
* [System](systems.md#--system-role-of-a-system)
* [System](systems.md#--behavior-of-the-system) (behavior of)
* [System](systems.md#--system-role-of-a-system) (role)
* [System](systems.md#--state-of-the-system) (state of)
* [Task](systems.md#--task)
* [Text](code-snippets-tmp.md#--texts-and-characters)
* [Understanding](understanding.md#--reference-understanding) (of code snippets)
* [Understanding](understanding.md#--behavior-prediction-and-understanding) (of reference behavior)
* [Understanding](understanding.md#--role-understanding-of-declared-or-imported-references) (of reference role)
* [Unit test](code-snippets-tmp.md#--unit-test)
* [Word](code-snippets-tmp.md#--programming-language-alphabet-word)
