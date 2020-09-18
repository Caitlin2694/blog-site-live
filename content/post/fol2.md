---
date: 2020-09-18
archives: "2020"
linktitle: An Introduction to First Order Logic (for Engineers)
title: An Introduction to First Order Logic (for Engineers)
tags: [ "ontology", "first-order logic", "engineering" ] 
weight: 30
draft: false
markup: mmark
---

This is our first blog on the technical aspects of ontologies for engineers. We have taken inspiration from many sources and have created examples relevant to an engineering/maintenance context.

# First Order Logic
**First Order Logic (FOL)** is a mathematical knowledge representation language used to describe logical concepts and relationships. FOL has many applications. The motivations for using FOL are the unambiguous representation of concepts and the representation of reasoning (how an argument can be represented as a FOL proof). 

Computers are very good at processing logic at scale and fast. We use this capability to process data, especially for problems that involve reasoning. Reasoning involves rules such as if-then statements and the knowledge of hierarchies (e.g. knowing a bearing is a part of a pump). For a computer to reason, relationships and constraints need to be made explicit. We can use ontologies to capture knowledge in specific domains and then apply reasoning to make inferences. Ontologies are built by defining concepts, relationships and axioms  — FOL can be employed for this purpose.

For example, a computer does not know that an electric motor is a type of motor. We need to tell this to the computer explicitly. A FOL statement for this is: $$\forall x (ElectricMotor(x) \longrightarrow Motor(x))$$

With a little training, provided here in this blog, we want to help engineers learn to read these statements. This will enable engineers to collaborate with the computer scientists responsible for translating their requirements into the ontologies that automate reasoning about their equipment. Our research group deals primarily with industrial maintenance, therefore the following examples are drawn from this domain.

## Elements of FOL

FOL uses **predicates** to represent facts about **entities** and the relationships between them.   **Logical symbols** are used to make logical statements.

## Motivating examples

### A simple hierarchy
Let's consider a scenario in which we wish to reason about the functionality of system components.

In engineering, the concept of function is very important. Every engineering system has a function. This is what the owner or operator of the system wants the system to do. For example, the steering system on a bicycle has the function to provide directional control of bike whilst moving. The following statements capture this.

$$mechanicalSystem(x) \longrightarrow functionalObject(x)$$

$$functionalObject(x) \longrightarrow object(x)$$

The first line says that if $x$ is a mechanical system then $x$ is a functional object. 

The 2nd says that if $x$  is a functional object then $x$ is an object. An object may have its own FOL description within the ontology.

In these FOL statements, $mechanicalSystem$, $functionalObject$ and $object$ are all examples of **unary predicates**, which  represent a fact about a single argument. For example, $object(x)$ uses the $object$ **unary predicate** to express that the **entity** $x$, which is its single argument, is an object. 

It's worth examining a couple of terms used above. The use of the term **"argument"** in the last sentence may be ambiguous. In this context, an argument is an entity which a predicate "takes" or "describes". Its meaning is synonymous with function parameters in computer science.

We take **"entity"** to mean the same thing it does in everyday speech --- an object/thing/idea. [TO DISCUSS]  When we are making a statement about particular entities and not employing quantifiers, the symbols we use to discuss entities are **constants**. However, if we are using quantifiers to make statements about all entities as a whole, the symbols used are **variables**.

### Relationships between entities

However, we also need to represent relationships. For example, $hasFunction(x,y)$ states that the $hasFunction$ **binary predicate** relates the entity $x$ to the entity $y$ by stating that $x$ has the function $y$.

Consistency checking of data, a part of quality control,  is very important in engineering systems. In this case, we wish to check that every system has a defined function. We can use the computer to check this by requiring the following:
$$\forall x (system(x) \longrightarrow \exists y (function(y) \land hasFunction(x,y)))$$

In English, we read this as "for every x ($\forall x$) that is a system ($system(x)$), there exists some y ($\exists y$) where y is a function ($function(y)$) and ($\land$) x has the function y($hasFunction(x,y)$"). More simply, for each system there exists at least one function which the system has. 

The fact that a single line can be used to make a statement about all systems in our domain is powerful. The alternative is to have many rules defining the relationships between individual systems and their functions.

Here, $\longrightarrow$ is the *implication symbol*. For $a \longrightarrow b$ to be true, it must be the case that whenever $a$ is true, $b$ is true.
For cases where $a$ is not true, $b$ may be true or false. $a \longrightarrow b$ is true unless $a$ is true and $b$ is false. For example, for $isBentShaft(x) \longrightarrow isFailedShaft(x)$  to be true, it must be the case that whenever a shaft is bent it fails. However,  if a shaft fails, it is not necessarily because it was bent (it may fail due to torsion).

$\longrightarrow$ is a *binary connective*, the main type of **logical symbol**. *Binary connectives* connect two logical statements into a single statement which can be evaluated as true or false depending on the conditions of the connective. As explained above, the condition of $a \longrightarrow b$ being true is that either $b$ is true or $a$ is false. 

In the above formula, $\forall x (system(x) \longrightarrow \exists y (function(y) \land hasFunction(x,y)))$, $\forall$ is also used. $\forall$ is a *quantifier*, another type of **logical symbol**. *Quantifiers* are used to make logical statements which connect all entities, rather than individual ones. The $\forall$ quantifier is the *for all quantifier*. $\forall x (P(x) \longrightarrow Q(x))$ is a true statement if for all entities $x$ where $P(x)$ is true, $Q(x)$ is also true.

Quantifiers will be further explained in a future blog.

## Predicates
**Predicates** are used to express facts and/or relationships about their arguments. In particular, a **n-ary predicate** (i.e. a predicate of n valence/arity) is a predicate which takes n arguments. For example, a predicate of arity 1, such as $P(x)$ is a **unary predicate**. $P(x, y)$ is a **binary predicate** (of arity 2) and $P(x, y, z)$ is a **ternary predicate** (of arity 3). An extended list of arities can be found [here](https://oeis.org/wiki/Arity).

Figure 1 demonstrates the arity (number of arguments) of unary, binary and ternary predicates. 

![Example image](/img/blog-images/blog_4_fig_1.svg)
*Figure 1: Predicates and their number of arguments*

Let's say we wish to build a set of predicates to represent the functionality and maintenance needs of site equipment. Useful unary predicates are $system$ and $function$, which can be used to assert something is a system or a function, respectively. For example, if variable $x$ in $system(x)$ takes on the specific physical item  ($compressor323$), then we could assert that compressor323 is a system: $$system(compressor323)$$ and  that increasing pressure is a function:$$function(increasePressure)$$

While unary predicates are used to express facts about individuals like class membership, binary predicates can be used to express facts about the relationship between two individuals. For example, we could assert that a function of compressor323 is increasing pressure through the $hasFunction$ binary predicate: $$hasFunction(compressor323, increasePressure)$$

A common use of ternary predicates is to represent temporal information. For example, if we wish that compressor323 cracked at the time of writing, we could express this as:$$faultOccured(compressor323, cracked, 20200716T101107Z)$$

While unary, binary and ternary predicates are most common, there are applications of quaternary predicates, quinary predicates, and more. 

## Logical connectives in-depth

*Logical connectives* (a type of **logical symbol**) connect a number of logical statements into a single statement which can be evaluated as true or false. Whether the single statement is true or false depends on the conditions of the relevant connective. Most, but not all logical connectives are **binary connectives** which connect two statements. 

Figure 2 demonstrates how logical connectives can combine multiple logical statements into a single logical statement.

![Example image](/img/blog-images/blog_4_fig_2.svg)
*Figure 2: A binary connective combining two logical statements*

A common binary connective is $\land$, the conjunction or AND symbol. $a \land b$ is true when both $a$ and $b$ are true. For example, we could capture all physical systems as being both a physical object and a system with: $$physicalSystem(x) \equiv system(x) \land physicalObject(x)$$ The equivalence symbol, $\equiv$, can often be ambiguous in meaning (see "Note 1" below). For this blog, it can be interpreted as indicating that the statement on the left-hand side of $\equiv$ is synonymous with the statement on its right-hand side.  Above, the equivalence symbol indicates that the definition of a physical system is something that is both a system and a physical object.

We can represent the conditions in which $a \land b$ is true in a "truth table":

$a$ | $b$ | $$a \land b$$
 --- | --- | ---
False (0)| False (0)| False (0)
False (0)| True (1)| False (0)
True (1)| False (0)| False (0)
True (1)| True (1)| True (1)


We are showing you this as it helps you to unpack what is happening at the most granular level of logic. Truth tables are a useful technique to enumerate the possibilities for the truth of a statement.

We can represent a binary connective using Python, a programming language. Below each connective, we give a snippet with the analogous Python logic for experimentation. You can paste this into a Python editor to explore for yourself. 

```python colab_type="code" id="y7FOd1KWV9Np" colab={"base_uri": "https://localhost:8080/", "height": 34} outputId="050ae4c1-b75c-4909-c0fb-3f77b675990f"
a = False # Set me to True or False
b = False # Set me to True or False

print(f"The statement  {a} ∧ {b}  is {a and b}") # I print the truth of the statement a ∧ b
```

While the $\land$ binary connective requires both of its arguments to be true, the $\lor$ disjunction or OR symbol requires only one of its arguments to be true. That is, $a \lor b$ is true if $a$ is true or $b$ is true. For example, we can represent the fact that a machine needs technical attention if a fault has occurred or maintenance is due with: $$needsAttention(x) \equiv faultOccured(x) \lor maintenanceDue(x)$$

Below is the truth table for $\lor$:

$a$ | $b$ | $$a \lor b$$
 --- | --- | ---
False (0)| False (0)| False (0)
False (0)| True (1)| True (1)
True (1)| False (0)| True (1)
True (1)| True (1)| True (1)

```python colab_type="code" id="aAX4g92wV_S_" colab={"base_uri": "https://localhost:8080/", "height": 34} outputId="f0ee61ed-5325-4da1-d0b8-1bc949042e40"
a = False # Set me to True or False
b = False # Set me to True or False

print(f"The statement  {a} ∨ {b}  is {a or b}") # I print the truth of the statement a ∨ b
```

Many engineers find truth tables for $a \land b$ and  $a \lor b$ fairly intuitive. Truth tables also exist for the implication($\longrightarrow$) and bi-directional ($\longleftrightarrow$) symbols. This is explored below.

As noted earlier, a common binary connective is $\longrightarrow$, the implication symbol.  $a \longrightarrow b$ means that if $a$ is true then $b$ must be true. For example, we could represent the fact that if $x$ is a trompe (an old model of compressor) then $x$ is a compressor as: $$trompe(x) \longrightarrow compressor(x)$$ This statement is true unless $trompe(x)$ is true and $compressor(x)$ is false. Notably, *$a \longrightarrow b$ is always true if $a$ is false*.

Below is the truth table for $\longrightarrow$:

$a$ | $b$ | $$a \longrightarrow b$$
 --- | --- | ---
False (0)| False (0)| True (1)
False (0)| True (1)| True (1)
True (1)| False (0)| False (0)
True (1)| True (1)| True (1)


```python colab_type="code" id="g-GyXZYwVP_W" colab={"base_uri": "https://localhost:8080/", "height": 34} outputId="74778089-ffe4-4bff-b539-d080b2e205bb"
a = False # Set me to True or False
b = False # Set me to True or False

print(f"The statement  {a} ⟶ {b}  is {a == b or b}") # I print the truth of the statement a ⟶ b
```

The final common binary connective is $\longleftrightarrow$, the bidirectional or material equivalence symbol. $a \longleftrightarrow b$ is true if $a$ and $b$ have the same logical value. For example, we could represent the idea that the armature $x$ in brushed DC motors is the rotor with: $$inBrushedDCMotor(x) \land armature(x) \longleftrightarrow inBrushedDCMotor(x) \land rotor(x)$$ This is because, in a brushed DC motor, the armature rotates making it a rotor, but in other motors it can be stationary, making it a stator rather than a rotor. 

Below is the truth table for $\longleftrightarrow$:

$a$ | $b$ | $$a \longleftrightarrow b$$
 --- | --- | ---
False (0)| False (0)| True (1)
False (0)| True (1)| False (0)
True (1)| False (0)| False (0)
True (1)| True (1)| True (1)

```python colab_type="code" id="ZKPivZorbnoL" colab={"base_uri": "https://localhost:8080/", "height": 34} outputId="c63f03fc-2c19-426c-8aec-b432f1ec630e"
a = False # Set me to True or False
b = False # Set me to True or False

print(f"The statement  {a} ⟷ {b}  is {a == b}") # I print the truth of the statement a ⟷ b
```

Logical connectives are primarily, but not exclusively, binary connectives. One exception is $\lnot$, the negation symbol, a *unary connective*. $\lnot a$ is true when $a$ is false. This can be interpreted as the "NOT symbol". For example, $\lnot a$ is read as "not a ".

Below is the truth table for $\lnot$:

$a$ | $$ \lnot a$$
 --- | ---
False (0)| True (1)
True (1) | False (0)

```python colab_type="code" id="nIst7t8XbwqH" colab={"base_uri": "https://localhost:8080/", "height": 34} outputId="b48e3e09-0633-4f0d-dc70-49ff463dc5ed"
a = False # Set me to True or False

print(f"The statement  ¬{a} is {not a}") # I print the truth of the statement ¬a

```

### Note 1: $\equiv$
There are cases where $\equiv$ is entirely logical (for every grounding of variables, whenever the left side is true, the right side is true). There are also cases where $\equiv$ is used to define an abbreviation or constrain the interpretation of a predicate, but these should be justified in the context of the semantics of the system, and in most cases, these reduce to logical expressions.

### Note 2
"Grounding is the task of taking a problem specification, together with an instance and producing a variable-free first-order formula representing the solutions to the instance" (Aavani, Amir, et al. "Grounding formulas with complex terms." _Canadian Conference on Artificial Intelligence_. Springer, Berlin, Heidelberg, 2011).


## More information

Another useful concept, often introduced with truth tables is the idea of validity. An introduction to validity and truth tables can be found at https://bookdown.org/rlridenour/ct-text/truth-tables.html#truth-tables-and-validity or in [this video](https://www.youtube.com/watch?v=ePmXbBvXxP8).

In a future post, we will explore FOL quantifiers in greater depth. 

For any questions or comments please contact [Marcus Handley](https://www.linkedin.com/in/marcus-handley-a2a6b1179/), marcus.w.handley@gmail.com or [Caitlin Woods](https://www.linkedin.com/in/caitlin-woods/), caitlin.woods@research.uwa.edu.au.  Written by [Marcus Handley](https://www.linkedin.com/in/marcus-handley-a2a6b1179/), edited by [Caitlin Woods](https://www.linkedin.com/in/caitlin-woods/), [Emily Low](https://www.linkedin.com/in/emily-low-1501/), [Frinze Lapuz](https://www.linkedin.com/in/frinze-erin-lapuz/) and  [Melinda Hodkiewicz](https://www.linkedin.com/in/melinda-hodkiewicz-b6bbba7/). We would like to acknowledge the helpful comments of [Tim French](https://www.linkedin.com/in/tim-french-3881208/)

