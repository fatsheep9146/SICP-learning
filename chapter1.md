# 1 Building Abstractions with Produces

The basic of Lisp

- expressions
- naming
- compound procedure

## 1.1 The element of programing

The essence of a programming language: 

- combine simple ideas to form complex ideas to solve the problems in reality.

3 mechanisms to accomplish this:

- primitive expressions: which represents the simpliest entities the language is concerned with,
- means of combination: by which compound elements are build from simpler ones.
- means of abstraction: by which compound elements can be named and manipulated as unit.

2 kinds of elements that languages concern

- data
- procedures

### 1.1.1 Expressions

Primitive expressions are already a basic means of combination

Lisp basic expressions

```
(operator, operands..)
```

for example 

```
(+ 1 2 10 11)
24
```

Expressions such as these, formed by delimiting a list of expressions within parentheses in order to denote procedure application, are called combinations. 

And the convention of placing the operator to the left of operands is called prefix notation. 

### 1.1.2 Naming and The environment

`define` is a basic and important way of abstractions.

syntax

```c
(define size 2) 
```

It should be clear that the possibility of associating values with symbols and later retrieving them means that the interpreter must maintain some sort of memory that keeps track of the name-object pairs.  This memory is called the environment is memory is called the environment (more precisely the global environment,

### 1.1.3 Evaluating the combination

### 1.1.4 Compound Produces

with the basic combination method in 1.1.1 —— primitive expressions(or primitive procedures)

and the basic abstractions method in 1.1.2 —— naming a variable 

we can introduction a more complex abstraction method —— procedure definition or (compound procedure)

the syntax is 

```lisp
(define (⟨name⟩ ⟨formal parameters⟩) ⟨body⟩)
```

for example

```lisp
(define (square x) (* x x))
```

### 1.1.5 The substitution modal for procedure application

The method of evaluating the compound procedures consist of two different implemetation 

- applicative order
    - evaluate the arguments and then apply
- normal order
    - fully expand and then reduce

Lisps choose applicative order.

### 1.1.6 Conditional Expressions and Predicates

For case analysis demand, lisp provides two  operator,

- cond
- if

cond syntax

```lisp
(cond (⟨p1⟩ ⟨e1⟩) 
			(⟨p2⟩ ⟨e2⟩)
			...
			<(else <en>)>)
```

- p is called predicate
- e is called expressions

all predicates are evaluated one by one, until it found the predicate is evaluated to be true.

if syntax

```lisp
(if <predicate> <consiquence> <alternative>)
```

For predicate , lisp provides several primitive operator

- < > =
- and, or, not

### 1.1.8 Procedures as Black-Box Abstractions

a procedure definition should be able to suppress detail. The users of the procedure may not have written the procedure themselves, but may have obtained it from another programmer as a black box.

Advanced Details in procedure definition

- local names (by formal parameters)
    - A procedure’s implementation that should not matter to the user of the procedure is the implementer’s choice of names for the procedure’s formal parameters.
    - Formal parameters can be used as local names in the scope of procedure body.
- internal procedure definition
    - procedure definition can be nested in other procedure

```go
(define (parent x)
	(define (child x y)
		(+ x y)
	)
	(child x 1.0)
)
```

- lexical scoping
    - formal parameter in parent procedure can be used as free variable in nested sub functions

```go
(define (parent x)
	(define (child y)
		(+ x y)
	)
	(child 1.0)
)
```

## 1.2 Procedures and the Processes They generate

In this section, we will examine several conventional procedure patterns. 

We will also investigate the rates at which these processes consume the important computational resources of time and space.

### 1.2.1 Linear Recursion and Iteration

Recursive process: 

- the process which is characterized by a chain of deferred operations
- this process requires that the interpreter keep track of the operations to be performed later on

For example, following procedure is recursive process:

```lisp
(define (factorial n)
	(if (= n 1)
		1
		(* (factorial (- n 1)))
	)
)
```

Iterative process: 

- one whose state can be summarized by a fixed number of state variables, together with a fixed rule that describes how the state variables should be updated as the process moves from state to state and an (optional) end test that specifies conditions under which the process should terminate

For example, following procedure is iterative process:

```lisp
(define (factorial n)
	(fact-iter 1 1 n)
)

(define (fact-iter product counter max-count)
	(if (> counter max-count)
		product
		(fact-iter (* product counter)
							 (+ counter 1)	
							 max-count							
		)
	)
)
```
