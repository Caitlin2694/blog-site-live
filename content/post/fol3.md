---
date: 2020-09-18
archives: "2020"
linktitle: Quantifiers in-depth (for Engineers)
title: Quantifiers in-depth (for Engineers)
tags: [ "ontology", "first-order logic", "engineering", "quantifiers"] 
weight: 30
markup: mmark
draft: false
---

## Introduction
In [our prior post](/post/fol2) we discussed *First Order Logic (FOL)*, a useful language for knowledge representation.

For example, the following FOL statement expresses that that an electric motor is a type of motor: $$\forall x (ElectricMotor(x) \longrightarrow Motor(x))$$ In greater detail, this can be read as _for every possible x_ ($$\forall x$$) _x being an electric motor_ ($$ElectricMotor(x)$$) _implies_ ($$\longrightarrow$$) _x is a motor_ ($$Motor(x)$$). In this statement, $$ElectricMotor$$ and $$Motor$$ are **predicates**, $$x$$ is a **variable** and both $$\forall$$ and $$\longrightarrow$$ are **logical symbols**.

There are two types of **logical symbols**. The first, which we detailed [previously](/post/fol2) are *logical connectives*, which include *binary connectives* such as $$\longrightarrow$$. The other type is *quantifiers*, such as $$\forall$$.

*Quantifiers* are used to make logical statements about the quantity of entities that satisfy an expression. The $$\forall$$ _for all_ quantifier makes a statement that all entities satisfy an expression. The $$\exists$$ _there exists_ quantifier makes a statement that at least one entity satisfies an expression.

## For all

The $$\forall$$ quantifier is the _For All_ quantifier. $$\forall x (P(x) )$$ is a true statement if for all entities $$x$$,  $$P(x)$$ is true. 

Consider the predicates $$component$$ and $$materialEntity$$. In FOL, the statement $$\forall x (materialEntity(x))$$ means that everything is a material entity. In an engineering context, this is incorrect as some things, like processes, are not material entities.  A  more plausible statement would be that all components are material entities. This is  written as $$\forall x (component(x) \longrightarrow materialEntity(x))$$. Given the definition of $$\longrightarrow$$, the previous statement makes no comment on whether non-components are material entities or not. This is as $$a \longrightarrow b$$ is always true if $$a$$ is false. 

If we were to use the bidirectional connective and wrote $$\forall x (component(x) \longleftrightarrow materialEntity(x))$$ this would not be a true statement in an engineering context, as not all material entities are components. 

As $$\forall x P(x)$$ represents that $$P(x)$$ is true for all $$x$$,  we can expand this to: $$\forall x P(x) \equiv P(x_1) \land P(x_2) \land P(x_3) \land \ldots \land P(x_n)$$, where $$x_1, x_2, x_3, \ldots , x_n$$ represents all entities. This is a powerful concept, showing that the $$\forall$$ quantifier can be seen as a chain of conjunctions. 

## There exists

As described above, statements with the $$\forall$$ _for all_ quantifier are used to state that something is true for all entities. Now we outline $$\exists$$,  the _there exists_ quantifier. $$\exists$$ is used to state that there exists (at least) one entity which makes the statement it contains true. That is, $$\exists x (P(x))$$ is true if there exists some entity x such that $$P(x)$$ is true.

Let us consider the $$materialEntity$$ and $$component$$ predicates from earlier. To express the statement that there is at least one material entity, we would write $$\exists x(materialEntity(x))$$. To express that there is at least one component that is a material entity, we would write $$\exists x (component(x) \land materialEntity(x))$$. 

Often in FOL, there are multiple ways of expressing the same idea. For example, there are many ways of expressing that there is a material entity that is not a component. We could sensibly write $$\exists x (materialEntity(x) \land \lnot component(x))$$.  Alternatively we could write $$\lnot \forall x (materialEntity(x) \longrightarrow component(x))$$. In English, these are read as "there exists some $$x$$ such that $$x$$ is a material entity and $$x$$ is not a component" and "it is not the case that for all x if $$x$$ is a material entity then $$x$$ is a component" respectively.

As $$\exists x P(x)$$ represents that $$P(x)$$ is true for some $$x$$, $$\exists x P(x) \equiv P(x_1) \lor P(x_2) \lor P(x_3) \lor \ldots \lor P(x_n)$$. Similar to showing that the $$\forall$$ quantifier can be seen as a chain of conjunctions, this shows that the $$\exists$$ quantifier can be seen as a chain of disjunctions. 

##  Domain of discourse

When quantifiers and variables are used to make statements about all entities, the statements are being made about all entities within a **domain of discourse**. The domain of discourse is the collection of entities that our logic is considering and making statements about. 

In this blog the domain of discourse is often implied to be the entities of an industrial site --- it would include specific compressors ($$compressor323$$) but not pizzas. However, in most formal logic contexts, it will be clearly defined.

## Conclusion

FOL is very useful and can express a large variety of ideas. As a result, it is often employed in academic texts.  However, its expressivity can be a hindrance to reasoning, limiting its application to computing. To the rescue are Description Logics, discussed in the next blog post. 

For any questions or comments please contact [Marcus Handley](https://www.linkedin.com/in/marcus-handley-a2a6b1179/), marcus.w.handley@gmail.com or [Caitlin Woods](https://www.linkedin.com/in/caitlin-woods/), caitlin.woods@research.uwa.edu.au.  Written by [Marcus Handley](https://www.linkedin.com/in/marcus-handley-a2a6b1179/), edited by [Caitlin Woods](https://www.linkedin.com/in/caitlin-woods/), [Emily Low](https://www.linkedin.com/in/emily-low-1501/), [Frinze Lapuz](https://www.linkedin.com/in/frinze-erin-lapuz/) and  [Melinda Hodkiewicz](https://www.linkedin.com/in/melinda-hodkiewicz-b6bbba7/).  We would like to acknowledge the helpful comments of [Tim French](https://www.linkedin.com/in/tim-french-3881208/)


