---
title: "Trade-Offs on Monolith vs. Distributed Architectures"
Description: "If you’re thinking about breaking your monolith into microservices, this article may be for you"
tags: ['Software Architecture', 'Microservices']
date: 2022-09-13
---
These days there is much talking about distributed architectures and event-sourcing models, especially in cloud infrastructures and Kubernetes clusters. It has gained a lot of momentum in the last few years, and it may look for some people that is the ultimate solution for their architecture coupling and scalability problems. I’ve been reading about it in the last weeks, and I thought about sharing my considerations on it.

If you’re considering breaking your monolith into microservices, this article may be for you. I’ll try to dissect the trade-offs and defend the monolithic approach for some situations under certain practices.

![Contrete building](./img/patrick-robert-doyle-_8bM_EqmFgM-unsplash_cropped.jpg)
Photo by Patrick Robert Doyle on [Unsplash](https://unsplash.com/photos/white-and-gray-concrete-building-_8bM_EqmFgM?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

## Definitions
First, what is distributed architecture? Is there a difference between the distributed system? And what is considered a monolithic or a microservices architecture?

You can skip this section if you’re already familiarized with these terms. If not, let’s define these concepts to get rid of ambiguities.

Also, I’ve seen disagreement on the internet around some of these definitions, so I wrote down my references in the last section.

### Distributed System
First, let’s introduce a technical definition and then summarize it.

>“A distributed system is an application that executes a collection of protocols to coordinate the actions of multiple processes on a network, such that all components cooperate together to perform a single or small set of related tasks.”
>— Definition from the University of Washington. [^1]

So, a distributed system is just a group of machines connected through remote access protocols to perform a task.

A client-server architecture is an example of a distributed system. In the most basic web application, you connect to the server through HTTP to fetch the web page.

### Monolithic architecture
It’s common to think of a monolithic architecture as a single piece of the coupled codebase for your entire app living in the same machine, but we have to keep in mind that all the systems we categorize as “monolithic” are probably also distributed systems if we are rigorous. A simple nonstatic webpage will most likely be read from a database in another machine. So we will not define it just based on how many machines are involved in the system.

>“An architecture is monolithic when all the code is a single unit of deployment.”
>— From the book “Fundamentals of Software Architecture.” — O’Reilly. [^2]

That’s the classic definition, and it’s a good one, but let’s clarify some things.

The monolithic nature of a system depends on your scope to determine it. This means your whole system could not be monolithic, but your back or frontend could. So, besides the monolithic architecture, I want to talk about monolithic components.

And I rely on this statement in the broad software architecture literature because everyone talks about the monolithic nature of single layers of a system. For example, Sam Newman discusses the monolithic user interface layer in microservices. [^3]

So, knowing you can talk about the architecture of specific layers, even if you have your frontend and backend decoupled using a REST API, there could be a monolithic frontend and a monolithic backend connecting to a monolithic database — because all three are single units of deployment.

### Distributed architecture
Well, thinking of the definition of monolith architecture, we could define the distributed architecture definition by the negative.

>“A distributed architecture is a group of deployment units connected through remote access protocols.”
>— From the book “Fundamentals of Software Architecture,” O’Reilly. [^2]

This applies to any layer of an application too. For example, your backend could be a group of services running on different machines, each containing one of your domain logic pieces. Or a database could be distributed if it runs on several machines through sharding, redundancy systems, and load balancers.

### Microservices
Microservices architecture is a type of [Service-Oriented architecture](https://en.wikipedia.org/wiki/Service-oriented_architecture). This means the codebase is built across multiple distributed services. Microservices have the particularity of including their own encapsulated database in each service. It’s heavily based on Domain Driven Design (DDD), so the services are built based on the idea of DDD’s Bounded Context. One of this architecture’s core ideas is that every microservice is independently deployable and not coupled to the others.

{{< figure src="./img/microservices-architecture.png" alt="Microservices architecture" position="center" caption="Microservices architecture" caption-class="center" >}}

## Why Would You Want Microservices?
The main reasons are the extreme scalability and flexibility. When you divide your business logic around a lot of little uncoupled interchangeable pieces, you gain a level of plasticity difficult to accomplish any other way.

This scalability and flexibility come because of the following possibilities:

### Autoscale-specific use cases
Autoscale is a singular service depending on the load that it receives instead of scaling the entire machine (with the expensive costs that means). You could, for example, scale the payment service on demand and leave the other use cases untouched.

### Implementation independence
Write a microservice in any programming language and any database implementation and keep all that hidden from all the rest services.

This offers quite a lot of independence to the teams to use the right tools for each job and not be restricted to the company’s tech stack.

### Scoped crashes
Keep the failure scope controlled if one service doesn’t work as intended.

You can think of each service as an input/output API, and be sure that if the output is not the expected one, you’ll find the bug inside the service due to the encapsulation.

### Independent deployability
This is undoubtedly one of the most important features of the Microservices architecture. You can deploy each microservice independently so the deploys are lighter, more agile, and won’t break any other functionality outside the service. If you don’t achieve independent deployability, you’ll have a distributed monolith, which we’ll discuss later in this article.

## Avoid development collisions
You can have multiple teams working on several features with the sureness that the two developments would not collide or break each other’s code.

In a monolith, the scope of change comes across the entire app instead of being an isolated component connected to the others, as we can see in the images below, so the risk of breaking a common component is higher.


{{< figure src="./img/monolith-scope-of-change.png" alt="Scope of change in a monolithic application" position="center" caption="Scope of change in a monolithic application" caption-class="center" >}}

{{< figure src="./img/microservices-scope-of-change.png" alt="Scope of change in a microservices architecture" position="center" caption="Scope of change in a microservices architecture" caption-class="center" >}}

### Simpler contextualization

It can be easier for a developer to understand their part of the system instead of struggling with the whole project before performing a simple task.

### Fixes organizational silos
With microservices modeled around a business domain, you can properly align the business requirements with the IT architecture as its core instead of having product and dev departments that know nothing about each other.

>“In traditional IT organizations, the act of developing software is often handled by an entirely separate part of the business from that which actually defines requirements and has a connection with the customer.”
>— Sam Newman, Monolith to Microservices [^4]

This may have sounded familiar to you. In a lot of companies, the dev and product teams don’t understand why a specific set of requirements is set in any of the two directions. Sometimes we do things a particular way because the “product department has decided this way” or because the “devs department says that can’t be done this way,” and it’s legit to some point. But a moderator is needed in between that understands the two sides, and the traditional tech company organigram doesn’t facilitate this.

There is a famous saying in the IT industry related to this called Conway’s Law:

>“Any organization that designs a system will produce a design whose structure is a copy of the organization’s communication structure.”
>— Melvin E. Conway [^5]

That’s why the layered monolithic is so common in a lot of small companies, because they usually build their team based on their technical roles (database administrators, backend, frontend, etc.) instead of product responsibilities, and it works pretty well, but it’s not so scalable.

So that’s why the microservices approach seems more convenient at a larger scale to maximize the cohesion and communication in the organization teams, software architecture, and its relation with the client, as seen in these images below:

{{< layout >}}
    {{< column align="center" valign="center" >}}
      {{< image src="./img/it-business-silo.png" alt="IT/Business silo" position="center" >}}
    {{< /column >}}
    {{< column >}}
      {{< image src="./img/product-oriented-organization.png" alt="IT/Business silo" position="center" >}}
    {{< /column >}}
  {{< /layout >}}
An organizational view of the traditional IT/business divide (left) vs a more product-oriented approach.

## Why You Wouldn’t Want Microservices
As you may know, it adds a lot of complexity everywhere. The first group of issues are the well-known fallacies of distributed computing. These are a set of common assertions made by L Peter Deutsch and other colleagues at Sun Microsystems, and although you can find them in a monolithic architecture, too, in a distributed one, this is maximized.

Let’s summarize each one of them:

1. The network is reliable.
2. Latency is zero.
3. Bandwidth is infinite.
4. The network is secure.
5. Topology doesn’t change.
6. There is one administrator.
7. Transport cost is zero.
8. The network is homogeneous.

This is a wide topic, so I’ll direct you to this great article if you want to know more about it[^6]

Aside from these, this type of architecture can lead to the following complexities:

### Eventual consistency
Now, this can be hard; it’s one of the worst drawbacks of the microservices architecture. Due to the database sharding, you won’t be able to make ACID transactions. This can lead to data consistency problems, and you must synchronize your data to coordinate with other services.

{{< figure src="./img/microservices-foreign-database.png" alt="You can’t access a foreign database in microservices" position="center" caption="You can’t access a foreign database in microservices" caption-class="center" >}}

To do this, you have to access the foreign database from the microservice API. There are two main ways of accomplishing this:

Rely on a distributed transaction (or 2 Phase Commit), which is not suitable for high loads due to the latency.
Implement a SAGA pattern[^7], which adds a bunch of complexity to the transaction.[^8]


### Distributed observability
Monitoring gets more complex in a distributed application. Now you have to be watching logs and request metrics from many places, and you should try to centralize that. Otherwise, you’ll lose control over it.

It’s possible to configure your cloud service like CloudWatch to do that effectively, but there are more powerful tools like Elastic Stack, Grafana, or Prometheus for Kubernetes clusters.

### Contract maintenance and versioning
A contract is the shape of the data that are agreed upon between a service and its client to understand each other. An example would be the JSON parameters that have to be sent to a REST API to parse the request.

In microservices, it gets tricky because of the decoupled nature of the system and the number of services, so the contracts have to be versioned.

Each service must not break these versioned contracts until it’s known that no other microservice relies on a particular versioned contract. Also, remember that other microservices may need to roll back to a previous code version that requires a previous contract [^10].

## The Monolith
If we’re analyzing the trade-offs, we must know fairly well the monolithic approach and its types.

In summary, there are at least three types of monolithic systems:

- The single-process system.
- The modular monolith.
- The distributed monolith.

### The single-process monolith
This is a system in which all of the code is deployed as a single process, as you may see in the picture below. You may have multiple instances of this process for robustness or scaling reasons, but fundamentally, all the code is packed into a single process. They usually have weak or inexistent boundaries between the code modules. This approach is characterized by a high level of coupling, repeated code, and performance issues and can lead to a Big Ball of Mud.

{{< figure src="./img/single-process-monolith.png" alt="Single-process monolith" position="center" >}}


### The modular monolith
It is a subset of the single-process monolith. The difference is that each module can be worked on independently, but it still needs to be combined for deployment. It fixes the single process’s coupling and flexibility issues and can work well with TDD.

For many organizations, the modular monolith can be an excellent choice. If the module boundaries are well defined, it can allow a high degree of parallel working, organized code, and scalability.

There is even the idea of a decomposed database for individual modules; this can work very well for data-intensive applications and keeps the monolith’s simplicity fairly well.

{{< layout caption="Single-database monolith vs multi-database monolith." caption-position="center" >}}
    {{< column align="center" valign="center" >}}
      {{< image src="./img/modular-monolith-single-database.png" alt="Monolith with a single database" position="center" >}}
    {{< /column >}}
    {{< column >}}
      {{< image src="./img/modular-monolith-multiple-databases.png" alt="Monolith with multiple databases" position="center" >}}
    {{< /column >}}
  {{< /layout >}}

### The distributed monolith
>“A distributed monolith is a system that consists of multiple services, but for whatever reason, the entire system has to be deployed together.”
>— Sam Newman, Monolith to Microservices. [^9]

This happens when architecture is highly coupled, and you lose deployability independence. This can be one of the most inconvenient approaches because it has the disadvantages of a distributed system and the disadvantages of a single-process monolith.

## Why You Would Want a Monolith
Mainly because it’s way much simpler. They are simpler in development, infrastructure, and troubleshooting. Also, they simplify code reuse and data consistency.

The monolith has been systemically denigrated pretty unfairly because of comparing it to use cases that don’t belong to it. Monoliths are not designed for gigantic corporations and thousands of developers. Monolithic is a great choice for small/medium size projects, and as a temporal design choice, it all depends on examining the trade-offs.

A well-designed modular monolith could be clean, agile, and scalable, adopting methodologies like Clean Architectures, SOLID principles, TDD, and even DDD if there’s no coupling and the boundaries are well defined. The Shopify people tell us about their implementation of the Modular Monolith [^11] (although they use database sharding in Google Cloud) with (in their words) “one of the largest Ruby on Rails codebases in existence” and it seems it’s working for them.

So the blame does not ever belong to architecture; it belongs to the architects instead.

## Why You Wouldn’t Want a Monolith
As you work more in this architecture, you make the monolith bigger, and your team grows to the point where you end up getting in each other’s way. You’ll have teams waiting to change the same piece of code or deploy the whole monolith with their own new changes. With agile methodologies, this can work pretty nicely, but again at a larger scale, it can make the system unmanageable and lead to performance issues.

This type of problem can happen in a microservices architecture too, but this core idea of encapsulation and setting boundaries massively reduces the chances of getting conflicts.

## Conclusion
With all this said, I wanted to insist on one thing:

>There are no bad architecture types; there are bad architectural choices instead.

So, now that we’ve talked about the trade-offs, it’s time to think. The architecture for your systems is one of the things that, unfortunately, you can’t search in Google or Stack Overflow. You will have to find a balance.

I hope I have made things clearer. Let me know what trade-offs won’t let you sleep, and also leave a comment if I’ve left something out or I’m wrong anywhere. Feedback is appreciated.

Cheers!

[^1]: The Paul G. Allen School of Computer Science & Engineering: Course CSE490H: Computational Design and Fabrication. Introduction to Distributed Systems.

[^2]: Richards M., Ford N.,(2020) Fundamentals of Software Architecture (An Engineering approach), edited by O’Reilly Media Inc. Chapter “Monolithic Versus Distributed Architecture.”

[^3]: Newman S.,(2020) Monolith to Microservices, edited by O’Reilly Media Inc. Chapter 1: “Just Enough Microservices” — User Interfaces

[^4]: Newman S.,(2020) Monolith to Microservices, edited by O’Reilly Media Inc. Chapter 1: “Just Enough Microservices” — What problems Do They Create?

[^5]: Conway, Melvin E. (April 1968). “How do Committees Invent?”. Datamation. 14 (5): 28–31. Archived from the original on 2019–10–10. Retrieved 2019–10–10.

[^6]: Simple Oriented Architecture Blog, (2018). [Understanding the 8 fallacies of Distributed Systems](https://simpleorientedarchitecture.com/8-fallacies-of-distributed-systems/)
[^7]: microservices.io, [Pattern: Saga](https://microservices.io/patterns/data/saga.html)

[^8]: You can check this related article by Dilfuruz Kizilpinar, senior solutions architect at Garanti BBVA: [Data Consistency in Microservices Architecture](https://dilfuruz.medium.com/data-consistency-in-microservices-architecture-5c67e0f65256)

[^9]: Newman S.,(2020) Monolith to Microservices, edited by O’Reilly Media Inc. Chapter 1: “Just Enough Microservices” — The Monolith.

[^10]: Google Cloud documentation, (2022) Contracts, Addressing, and APIs for Microservices.

[^11]: Shopify’s Engineering Blog, (2019) Deconstructing the Monolith: Designing Software that Maximizes Developer Productivity.



