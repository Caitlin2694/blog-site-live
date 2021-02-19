---
date: 2021-02-18
archives: "2021"
linktitle: Description Logics (for Engineers)
title: Description Logics (for Engineers)
weight: 30
markup: mmark
draft: false
---

# Description Logics
## Why not First Order Logic (FOL)?
FOL, which we [explained previously](/2020/fol3/), is a knowledge representation language which can be used to express a variety of ideas. Expressivity is a measure of the modelling power of a knowledge representation language. 

The expressivity of FOL is a double-edged sword.

When trying to determine whether particular statements are true, more expressive knowledge representation languages require greater computational resources. FOL is *undecidable*, meaning that reasoning programs can't be written that are guaranteed to produce correct results without the possibility that they will never terminate (i.e. be stuck running _ad infinitum_). 

To move towards a knowledge representation language that has more desirable properties for computation, we introduce **Description Logic** (DL).

## DL vs FOL
DL has many parallels to FOL (the terminology used below is explained in [our earlier blog](/2020/fol2)):

- Where FOL has contraints/variables, DL has *individuals*.
- Where FOL has unary predicates (taking one argument), DL has *concepts*.
- Where FOL has binary predicates (taking two arguments), DL has *roles*.
 
DL also has notable differences to FOL:

- While FOL can have predicates of any arity (number of arguments), DL only has *concepts* to describe a single argument fitting a concept, and *roles* to describe one argument fulfilling a role to another.
- While FOL works with a small, flexible set of **logical symbols**, DL has a larger set of symbols with more restricted uses.
- There aren't particular types of FOL while DLs form a family of knowledge representation logics each with different functionality.
- In FOL any collection of "valid" statements is "allowed" while each DL has a specific set of restrictions, some of which don't apply to individual statements but combinations of multiple statements.
- DLs are usually decidable (while FOL is only semidecidable).
- In DL there is a custom (but not rule) of separating axioms into three separate "Boxes":
    * The Assertional Box (ABox) axioms capture knowledge about named individuals.
    * The Terminological Box (TBox) axioms capture knowledge about concepts and their relationship to one another.
    * The Relational Box (RBox) axioms capture knowledge about roles and their relationship to one another.

It may at first seem contradictory that while DLs are less expressive than FOL, they employ more symbols. While the common symbols of FOL are $$\forall \exists \land \lor \longrightarrow \longleftrightarrow () \equiv$$, those used in DLs include $$\forall \exists \sqcap \sqcup \circ  \top \bot $$ $$ U \lnot \sqsubseteq = {\dot = } : \leq \geq \{\}  () $$ $$  ^- \equiv \approx \not \approx Self $$ $$  Trans $$ $$  Disjoint$$ . 

While DLs have more symbols, they are each more constrained in their use. As a result,  DLs (often) have less expressivity than FOL but can express many ideas using fewer symbols. For example, to express the all electric motors are motors,  we would write this in FOL as: $$\forall x (ElectricMotor(x) \longrightarrow Motor(x))$$ In (most) DLs  we could write: $$ElectricMotor \sqsubseteq Motor$$


## A family of DLs


An in-depth explanation of DLs can be found here: <https://arxiv.org/pdf/1201.4089.pdf>.

DLs aim to capture that **individuals** belong to **concepts** and can be related to other individuals by **roles**. A **concept** can be thought of as a group which an individual may belong to.

There isn't a single DL, instead, there is a family of DLs which each allow different *expressions* and *axioms* to be used. The rest of this blog focuses on the set of commonly used, decidable DLs.

As a DL gains more class expressions and axioms, the set of scenarios the DL could describe, known as its **expressivity** increases. However, the more scenarios a DL can express, the harder it is to make decisions about the scenarios a set of statements describe. As a result, there are many DLs each with their expressivity and performance (how quickly reasoning can occur) tailored to particular tasks.

Each DL has its expressivity described in its name, normally a collection of letters with each corresponding to a particular set of functionality. Common DLs include:
 - $$\mathcal{SROIQ}$$, one of the most powerful DLs and the basis of OWL 2 DL and OWL 1.1. OWL is explained in a future blog.
 - $$\mathcal{EL^{++}}$$ a subset of $$\mathcal{SROIQ}$$ which is the basis of OWL 2 EL and is particularly optimised for ontologies with large numbers of concepts. The $$\mathcal{E}$$ comes from it allowing existential quantification but not universal quantification.
 - $$\mathcal{DLP}$$ the intersection of DLs and [Logic Programming](http://www.doc.ic.ac.uk/~cclw05/topics1/index.html). $$\mathcal{DLP}$$ is designed to capture rules including spatial and temporal information. $$\mathcal{DLP}$$ is the basis of OWL 2 RL and a subset of $$\mathcal{SROIQ}$$.
 - $$\mathcal{DL-Lite}$$ a DL designed for efficient evaluation of conjunctive queries (such as those created by JOIN in SQL) and evaluation of these queries by existing relational data systems. $$\mathcal{DL-Lite}$$ is the basis of OWL 2 QL and a subset of $$\mathcal{SROIQ}$$.
 - $$\mathcal{ALC}$$ a historically significant DL and the basis of any DL beginning with $$\mathcal{S}$$ or $$\mathcal{ALC}$$.

A table outlining the meaning of the letters used in $$\mathcal{SROIQ}$$, $$\mathcal{SHOIN}$$, $$\mathcal{EL^{++}}$$, $$\mathcal{ALC}$$ and more can be found [on wikipedia](https://en.wikipedia.org/wiki/Description_logic#Naming_convention).

## $$\mathcal{ALC}$$
The $$\mathcal{ALC}$$ DL is a historically important DL and the basis of many other DLs. Any DL that contains $$\mathcal{ALC}$$ or $$\mathcal{S}$$ is built upon the functionality of $$\mathcal{ALC}$$. $$\mathcal{ALC}$$ allows the creation of complex concepts through the following:
 - $${A \sqcap B}$$ creates a new concept through **concept intersection**. The members of this new concept are the members of both  concept$$A$$ and  concept$$B$$.
 - $${A \sqcup B}$$ creates a new concept through **concept union**. The members of this new concept are the members of concept $$A$$ and/or concept $$B$$.
 - $${\lnot A}$$ creates a new concept through **concept negation**. The members of this new concept are all individuals that are not members of concept $$A$$.
 - $${\forall R.C}$$, where $$R$$ is a role and $$C$$ is a concept,  creates a new concept through **universal quantification**. If a member of this new concept is related to an individual by the role $$R$$, that individual is a member of the concept $$C.$$ 
 - $${\exists R.C}$$, where $$R$$ is a role and $$C$$ is a concept, creates a new concept through **existential quantification**. Each member of this new concept is related to at least one individual in concept $$C$$ by the role $$R$$. 

As  with other DLs, $$\mathcal{ALC}$$ allows concepts, including complex concepts, to be combined. So, a concept could make use of several of the above symbols. For example, the concept of "pumps that have a rotor but do not have an impeller (an impeller is a type of rotor used in centrifugal pumps)" could be represented with either : 

$$pump \sqcap (\exists hasA.rotor) \sqcap (\lnot \exists hasA.impeller)$$
or
$$pump \sqcap \exists hasA.(rotor \sqcap \lnot impeller)$$
The first DL statement can be read as the individuals  which are a member of the pump concept ($$pump$$) and ($$\sqcap$$)  are a member of the concept "is related by the hasA role to a member of the rotor concept" ($$\exists hasA.rotor$$) and ($$\sqcap$$)  are not ($$\lnot$$) a member of the concept "is related by the hasA role to a member of the impeller concept" ($$\exists hasA.impeller$$).

The second DL statement can be read as the individuals  which are a member of the pump concept ($$pump$$) and ($$\sqcap$$)  are a member of the complex concept "is related by the $$hasA$$ role ($$\exists hasA.$$) to a member of the concept $$rotor \sqcap \lnot impeller$$". The concept $$rotor \sqcap \lnot impeller$$ can be read as individuals which are a member of the rotor concept ($$rotor$$) and ($$\sqcap$$) not ($$\lnot$$) a member  of the impeller concept ($$impeller$$).

Concepts are a building block of **axioms**. Axioms are how DLs represent knowledge. Different DLs allow different axioms. $$\mathcal{ALC}$$ allows the following axioms:
 - $${A \sqsubseteq B}$$ is called **concept inclusion**. It states that all members(individuals) of the concept $$A$$ are members of  the concept $$B$$.
 - $${a : B}$$ is called **concept assertion** and asserts that an individual $$a$$ is a member of the concept $$B$$. Alternatively, the notation $${B(a)}$$ can be used. This is interpreted in the same way as a unary predicate is in FOL. Unary predicates are outlined [in our FOL Blog](/2020/fol2)
 - $${(a,b): R}$$ is called **role assertion** and asserts that individual $$a$$ is related to individual $$b$$ by the role $$R$$. Alternatively, the notation $${B(a,b)}$$ can be used. This is interpreted in the same way as a binary predicate is in FOL. Binary predicates are outlined [in our FOL Blog](/2020/fol2)

 At first glance, you might be impressed by the expressive power of $$\mathcal{ALC}$$ and wonder what more is needed. While $$\mathcal{ALC}$$ affords us a lot of concept expressiveness, it has few tools to express complex role relationships.

One limitation is that $$ALC$$ has no ability to express **role transitivity**. This is the idea that if a role relates A to B and B to C, then that role should relate A to C. For example, we may wish to express that containership is transitive:  if a contains b and b contains c then a contains c. While in FOL we could write $$\forall a,b,c $$ $$ ( contains(a,b) \land contains(b,c) \longrightarrow contains(a,c))$$ $$\mathcal{ALC}$$ has no method of expressing this.  $$\mathcal{S}$$ represents the $$\mathcal{ALC}$$ DL with role transitivity, so DLs such as $$\mathcal{SHOIN}$$ or $$\mathcal{SROIQ}$$ can express this idea. 

## Conclusion
In this post, we covered the difference between FOL and DLs and outlined many common DLs, especially $$\mathcal{ALC}$$. In [the final blog post](CW: Link to final blog) we will go through **OWL**, a tool which is  used to computationally represent knowledge. For a detailed introduction to description logics, checkout ["A Description Logic Primer"](https://arxiv.org/pdf/1201.4089.pdf) by Markus Krötzsch, František Simančík and Ian Horrocks.

For any questions or comments please contact [Marcus Handley](https://www.linkedin.com/in/marcus-handley-a2a6b1179/), marcus.w.handley@gmail.com or [Caitlin Woods](https://www.linkedin.com/in/caitlin-woods/), caitlin.woods@research.uwa.edu.au.  Written by [Marcus Handley](https://www.linkedin.com/in/marcus-handley-a2a6b1179/), edited by [Caitlin Woods](https://www.linkedin.com/in/caitlin-woods/), [Emily Low](https://www.linkedin.com/in/emily-low-1501/), [Frinze Lapuz](https://www.linkedin.com/in/frinze-erin-lapuz/) and  [Melinda Hodkiewicz](https://www.linkedin.com/in/melinda-hodkiewicz-b6bbba7/). 

