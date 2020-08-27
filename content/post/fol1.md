---
date: 2020-08-20
archives: "2020"
linktitle: Representing Ontologies using First-Order Logic - Lessons Learned
title: Representing Ontologies using First-Order Logic - Lessons Learned
tags: [ "ontology", "first-order logic", ] 
weight: 30
draft: false
markup: mmark
---

# Representing Ontologies using First-Order Logic: Lessons Learned

Creating an ontology for your data has extraordinary benefits (see [here](/post/explain-boss) for an explanation).  When constructing a new ontology, it’s a good idea to do some preliminary work before constructing your model in an Ontology Development Environment (ODE) such as Protégé.

This preliminary work is as follows:
1. Identify the generic terms (or “concepts”) needed in your ontology. 
2. Discuss these terms and their definitions with a subject matter experts (SME).
3. Translate SME definition (written in natural language) to formal definitions (written in First-order logic).

The reason that natural language definitions (or “SME definitions”) are translated into formal definitions (or “FOL definitions”) is twofold. 
Firstly, it transforms the information into a format that the computer can understand, in-line with how the ontology will eventually be 
implemented (using RDF/OWL/CCL). Secondly, FOL definitions are more rigorous than SME definitions. 
These FOL definitions will help you to identify gaps in your SME definitions. 

This blog will share some of our team’s learnings from performing this translation in our work. 
We will explain why getting this translation right is so important as well as some common mistakes and tips. 
This blog will help you to take the first steps towards creating your own ontologies. 
Since our research group deals primarily in industrial maintenance, the examples used in this blog will be from the maintenance domain.

### Examples of SME definitions

SME definitions look like the definitions you might find in a dictionary, or the glossary of a textbook. For example:

Term | SME definition    
------------- | ---------- 
  Machine identifier | A unique identifier or serial number of a machine or asset. 
 Functional location  | Describes a physical location where a maintenance task is actioned. 

### Examples of FOL definitions

 Term | FOL definition   
 :------------- | ----------: 
 Machine identifier | *instanceOf(x,MachineIdentifier)≡ instanceOf(x,DescriptiveContentEntity∧ ∃y(instanceOf(y,Machine)∧denotes(x,y))∧∀z(denotes(x,z)→z=y)*
 Functional location  | *instanceOf(x,FunctionalLocation)≡instanceOf(x,DescriptiveContentEntity)∧ ∃y,z(instanceOf(y,MaintenanceTask)∧instanceOf(z,SpatialRegion)∧locationOf(z,y) ∧denotes(x,z))*

Although FOL definitions may appear foreign and difficult to understand, learning to understand them only requires (1)
 understanding what the following set of symbols mean, and (2) understanding how to match things denoted by x, y, z (etc.)
  to their descriptions. If you’re not familiar with FOL, keep an eye on future blogs for a beginner’s tutorial.


 Symbol | Meaning |
 :------------- | ----------: 
 ∧ | ‘and’ 
 ∨ | ‘or’ 
 →	 |‘implies’ 
 ↔ | ‘if and only if’ 
 ¬ | ‘not’ 
 ≡	| ‘equivalent to’ 

When matching things denoted by x, y, z (etc.) to their descriptions, a general rule of thumb is to apply what is 
included in the brackets to either side of the description, where the first entry in the bracket goes on the left 
side of the description, and the second entry in the bracket goes on the right side of the description. 
So, instanceOf(x,MachineIdentifier), would be interpreted as x (is an) InstanceOf (a) MachineIdentifier.
 Or, locationOf(z,y), would be interpreted as z (is the) locationOf y. Matching things denoted by x, y, z (etc.) 
 to their descriptions may seem unnatural at first, but with practice becomes easier. 

### Why is it important to get the translation right?

When translating SME definitions into FOL definitions, you want to make sure that the translation is sufficiently precise. 
That is, that all relevant SME definitions are consistent with the FOL definition, but no irrelevant SME definitions are.
 To understand why this they may not occur, consider the fact that every FOL definition has a direct English translation.
  Because a FOL definition is built using the symbols ∧, ∨, →, ↔, ¬, and ≡, its direct English translation will only have 
  ‘and’, ‘or’, ‘implies’, ‘if and only if’, ‘not’, and ‘equivalent to’ as the words connecting terms and phrases. 
  If your definition is not translated correctly into FOL, it is likely that mistakes will be made in the ontology’s
   implementation i.e. following its input into a computer. These mistakes are likely to cause reasoners to make incorrect inferences about your concepts. If this is the case, you will end up with an ontology that does not correctly reflect the real world.

### Translation as a collaborative process

For us, the translation of SME definitions to FOL definitions was a collaborative process. We had individuals with the following expertise in our team:
1.	A subject matter expert
2.	A computer scientist / ontology engineer
3.	A mathematician / logician

If you do not have all these people available, don’t worry! It is just worth knowing what these different areas of expertise bring 
to the table so that you know what you need to think about in the translation process. For us, a subject matter expert 
was important because we were working in a highly specialised industrial maintenance domain. The subject matter expert 
was able to highlight important concepts and clarify interpretations of those concepts. For example, they were able to
 provide examples of what would and wouldn’t work in the real world given our definition. Our mathematician / logician 
 understood the meaning of all the FOL symbols and how to string those together. Finally, our computer scientist / 
 ontology engineer was able to link our definitions to existing ontologies (for example, the BFO foundational ontology)
  and think about how our definitions would look as a machine-readable ontology.

### Common translation mistakes

As mentioned above, translation is a collaborative process. The advantage of having a team made up of members with 
different expertise is that they are likely to counteract different mistakes. In our team’s experience, once the subject
 matter expert provided a SME, the computer scientist/ontology engineer and mathematician/logician tended to pick up 
 on different shortcomings of proposed FOL definitions. The table below indicates who tended to pick up what.
 
 Computer scientist/ontology engineer | Mathematician/logician  
 :------------- | :---------- |
  (1)	Failure to integrate a FOL definition with existing ontologies, like the Relations Ontology (RO), that already includes relations like inheresIn, <br> (2) Inconsistencies and/or overlap between FOL definitions for different terms |  (1) Incorrect positioning of brackets, <br> (2) Using variable names inconsistently, <br> (3)Incorrect order of variables within a relationship i.e. locationOf(x,y) vs locationOf(y,x), <br> (4) Incorrect application of quantifiers 


Once our computer scientist and mathematician agreed on a FOL definition, the final step was always to take it back to 
the subject matter expert and check that it was suitable. As mentioned above, the way to do this is to make sure that
 the direct English translation is consistent with all appropriate SME definitions, and restrictive enough that it
  does not encompass inappropriate SME definitions. An example of a mistake that might be picked up here is definitions
   where an ‘and’ should be an ‘or’.  Keep an eye out for future blogs where instructions on how to avoid these common translation mistakes will be given.

### Lessons learned

1.	The translation process is an iterative process. The FOL definition is likely to uncover gaps your SME definition and vice versa. Multiple rounds of discussion may be required.
2.	Focus on what’s on the page rather than your understanding of what’s on the page. This applies when you’re translating the SME definition to the FOL definition, and when you’re checking back with the subject matter expert that your FOL definition is appropriate. An SME definition is not the implication of a FOL definition, but one plausible translation (perhaps among multiple) of a FOL definition.
3.	Test your logic with some examples from the real world. It is likely that you will find edge cases that need to be included in your definition.
4.	Show your logic to people outside of your team (who are familiar with logic but were not involved in its development) to ensure that others interpret your logic as intended.




We hope this blog was useful for you in your mission to start using ontologies in your organization. 
If you have questions, comments, or ideas about what we should write on next, please reach out to Caitlin at __caitlin.woods@research.uwa.edu.au__ or Emily at __emily.low@uwa.edu.au__.

Written by __Emily Low__ and __Caitlin Woods__

Research Assistants at __The UWA System Health Lab__
