---
date: 2020-06-23
archives: "2020"
linktitle: Explaining Ontologies to Your Boss
title: Explaining Ontologies to Your Boss
tags: [ "ontology", "reasoning", "interoperability", "vocabulary", "simple ontologies", ] 
weight: 30
draft: false
---

![Example image](/img/explain-boss-img.png)

<br/>
If you are a developer, software architect, or have worked in any data-focused organisation, you might have come across ontologies before. You may have heard about companies or research institutions who have leveraged ontologies to pull their data into a new age of “machine-readability”. If so, you could have tried to explain the benefits of this technology with your boss, only to be met with a blank face.

In fact, ontologies (in the context of computer science) appear to be notorious for their steep learning curve and high barrier to entry. In fact, it is easier to “sell” cutting-edge AI technology where information is scattered far and wide across the internet, then it is to sell ontologies. In my opinion, the reason for this has nothing to do with the technology itself. It comes down to a very simple and easily resolvable fact about the field of ontologies. Information about ontologies is incredibly difficult to decipher.

On the day you explained ontologies to your boss, it’s probable they liked what they were hearing. After your conversation, their mind was buzzing with ideas and opportunities about the technology. So, they went and typed “Ontology” into Google. When they clicked “Search” however, they were fronted with a tidal wave of different definitions and interpretations. Many of these are grounded in philosophy rather than computer science or information technology. At this point, you can’t blame your boss for not understanding how an ontology will fit into your business and it’s not surprising that this idea is abandoned.

This blog will be the first of (hopefully) many attempts to unveil some of the mysteries that hide ontologies away from outside onlookers. As someone who has worked in a research institution, it is my pleasure to open this mystifying field up and make it more accessible for people to use. This blog describes the three core benefits of ontologies. These benefits are __increased interoperability__, __automated reasoning__, and a __shared vocabulary__. These three points will help you to explain to your boss why ontologies are important for your business.

### 1) A Shared Vocabulary

Debates about what is meant by the an “ontology” in computer science continue well into 2020. The point that seems to be consistent across different definitions and interpretations is that an ontology should describe a shared vocabulary for a domain context. This means that the concepts (or “classes”) and the meaning of those concepts represented in an ontology, are agreed upon by domain experts. For example, an ontology may contain the concept of a “machine” and the meaning of the word “machine” is agreed and unambiguous. While this is one of the most solid and least debated features of ontologies, it is often a point that is overlooked in early ontology tutorials.

The value of ontologies representing a shared vocabulary is that it begins to break down “silos” both between software teams, within organizations and between organizations. It also means that if you would like to create an ontology for your business or context, you likely do not have to start from scratch. There are often existing ontologies that have been created by standards organizations or research groups that you can leverage. One such research group is the Industrial Ontology Foundry ( https://www.industrialontologies.org/ ) who are currently working on building an ontology as a shared vocabulary that can be used across industrial organizations such as mining, manufacturing or aviation. Another benefit of ontologies as a shared vocabulary is that it increases interoperability between the software applications that conform to this vocabulary. This is further described in point (2).



### 2) Increased Interoperability

For software engineers and information architects, increased interoperability is, in my opinion, the easiest selling point for ontologies. Ontology languages such as OWL (the Web Ontology Language) provide means to assert facts (or “axioms”) about each of the concepts (or “classes”) in your shared vocabulary. For example, an ontology engineer might describe a “parent” as something that has a “child”. In that case, you can assert an axiom that describes this relationship. This means that whenever a software application connects (or “conforms”) to an ontology, this relationship between the concepts of “parent” and “child” is explicit and cannot be mis-interpreted by the application. Therefore, when new applications are built, perhaps by different software teams, these concepts remain consistent across the different applications.

The value of this from your boss’s perspective is that increased interoperability decreases the amount of time and money spent debating how applications should communicate with each other. An obscene amount of time in software development projects is spent trying to “connect” new applications into an existing application landscape. Having an ontology to represent concepts in each application in a consistent way makes this process monumentally more efficient.

### 3) Automated Reasoning

If your boss is not yet convinced why ontologies are useful for your organization, you can now start talking about automated reasoning. This point is by far the most complex features of an ontology and the most difficult to explain quickly, but I am going to give it my best shot.

Automated reasoning is the ability for reasoners, that can be run over a defined ontology, to make interpretations (or “inferences”) about the information represented in the ontology. An example is if you have the concept of a “parent” in your ontology, and you define that a “parent of a parent” is also a “grandparent”. Therefore, if you have a piece of data (or “individual”) that is a “parent of a parent”, the reasoner could infer that the piece of data is also a “grandparent”. After this inference has been made, you can query for all “grandparents” in your system and retrieve the appropriate information. This is just one of many examples of the power of automated reasoning and it is worth diving into some more complex examples before trying to build your own.

I would like to stress that you must be careful when talking about automated reasoning. When you’re in a meeting, make sure that you understand the capabilities of the ontology language that you are using before making “magical” reasoning promises that you cannot keep. For ontologies, there is a tradeoff between expressivity (and in-turn reasoning capability) and performance. This is important to keep in mind when explaining ontologies to your boss.

The value of automated reasoning for your boss, is that it makes your data “smarter” and you can ask better questions of your data. Instead of requiring knowledge engineers to write complex queries every time you need a piece of information, simpler queries can be written. For example, without knowing how the data is represented in the system, a developer or a subject matter expert can ask the system to return all “grandparents” in a single, simple query.

<br/>


I hope this blog was useful for you in your mission to start using ontologies in your organization. If you have questions, comments, or ideas about what I should write on next, please reach out to me at __caitlin.woods@research.uwa.edu.au__

<br/>

Written by __Caitlin Woods__

Research Assistant at __The UWA System Health Lab__
