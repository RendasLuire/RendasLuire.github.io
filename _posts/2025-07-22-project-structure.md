---
layout: post
title: "Project Structure" 
date: 2025-07-22 10:00:00 -0600
categories: Learning daily
---

Before starting to code, I usually ask myself: *What should my project architecture look like?* I'm referring to the folder structure and how to organize components. It doesn't matter whether it's frontend or backend—I always ask myself this question.

So, I decided to do some research and study best practices. This post is the conclusion I've reached.

## How should I organize my code?

The goal is to make it easier to find components, so we need to **categorize our files into folders**. As the book *Clean Code* says, functions should do one thing only—and do it well. If we use that principle as our foundation, we can build clean and scalable projects.

Before this, I used to structure my backend projects like this:

`Model -> Controller -> Router`

It's a simple and common approach—and the frontend wasn't too different.

But best practices suggest a more modular structure, based on single responsibility principles. One commonly recommended structure, especially in backend projects, looks like this:

`Model -> Repository -> Service -> Controller -> Router`

Honestly, at first this sounded a bit strange to me, but I gave it a try—after all, those suggesting it have more experience than I do. I could only ask myself…

## What should go in each file?

Let's go step by step.

### Models

This stays mostly the same. Here, we define the structure of the entities we want to manage in our system. Models help us validate data and set default values, acting as a filter between our system and the database.

### Repositories

Next, we define how our system will interact with the database. In this layer, we write the methods to create, read, update, and delete data (CRUD). We can also add more complex or specific queries as needed.

This is very usefull specially in case that we need to change data resource like database.

### Services

This is where we put the **business logic**—how the data is processed after it’s received in a request and before it’s sent in a response. At this stage, we’re no longer dealing with raw data, but shaping it to fit our needs.

### Controllers

Controllers are responsible for handling the request and response. They perform basic validations on request parameters and return appropriate response codes depending on the outcome.

### Routers

Here we define the endpoints, grouping them by concept or resource. If necessary, we also apply middleware in this layer.

---

At first glance, all of this may seem tedious and over-engineered. It’s a lot of work to build a backend like this, and at an early stage it may not seem useful. But think long-term: as your system grows, this methodology becomes more and more important. It makes everything clearer—and in situations like testing, debugging, or maintaining your code, it truly pays off. All the extra effort will prove to be worth it.

In another post, I'll talk about testing—another topic I’ve been studying recently.

---


## References

- Robert C. Martin – Clean Code: A Handbook of Agile Software Craftsmanship
While it focuses on writing readable, maintainable code, many of its principles (like the Single Responsibility Principle) form the foundation for clean architecture and good project structure.
https://www.oreilly.com/library/view/clean-code-a/9780136083238/

- Node.js Best Practices – GitHub Repository
A curated list of best practices for Node.js development, including project structure suggestions.
https://github.com/goldbergyoni/nodebestpractices

- Domain-Driven Design – Eric Evans
A classic book that influenced modern layered architectures. Introduces the idea of separating business logic from infrastructure code.
https://domainlanguage.com/ddd/

- The Onion Architecture
A popular architectural pattern that inspired many backend structures similar to the one you describe.
https://jeffreypalermo.com/2008/07/the-onion-architecture-part-1/
