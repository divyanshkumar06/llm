# AI401 - Expert Systems Lab
## Knowledge Representation: Semantic Network with Inheritance

This document contains a complete breakdown, explanation, and Viva Q&A for the Python experiment on Semantic Networks and Frames.

---

### 1. Core Concepts Explained

#### A. What is a Semantic Network? (Part 1)
A Semantic Network represents knowledge as a directed graph. The computer memorizes facts using **Triples** structured as `(Subject, Relation, Object)`.
* Example: `("bird", "can", "fly")`

#### B. How does Inheritance work?
Inheritance allows a concept to automatically gain the properties of its parent category, saving memory and avoiding repetition. 
* We use the `is-a` relation for this. 
* Example: `penguin is-a bird`, `bird is-a animal`. 
* When asked if a penguin has skin, the algorithm doesn't find it directly in "penguin". It climbs the `is-a` chain to "bird", and then to "animal", where it finds `("animal", "has", "skin")`. This is a **bottom-up approach**.

#### C. Handling Exceptions (`cannot`)
Sometimes rules have exceptions (e.g., birds fly, but penguins don't).
* We handle this by adding specific negative relations like `("penguin", "cannot", "fly")`.
* Because the algorithm checks the local node (`penguin`) before moving up to the parent node (`bird`), the local exception is found first and overrides the inherited rule.

#### D. Extending the Network (Exercise 1)
To show how flexible semantic networks are, an **Ostrich** was added. By simply adding 3 lines of facts (`is-a bird`, `cannot fly`, `can run_fast`), the Ostrich automatically inherited all other bird and animal traits without explicitly coding them.

#### E. Frame-Based Representation (Exercise 2)
Instead of scattered triples, Frames group all properties of a specific object into a single dictionary (an object-like structure).
* `is-a` is replaced by the `ako` (A-Kind-Of) slot.
* Functionally, it works the same as the Semantic Network but is structurally more organized and compact.

#### F. Multiple Inheritance (Exercise 3)
When an object belongs to multiple categories (e.g., a **Bat** is both a `mammal` and a `flying_creature`), it inherits from multiple parents.
* **Conflict Resolution**: If parents have conflicting rules, the code uses **Breadth-First Search (BFS)** (linearization) to create a strict order. It ensures that the Bat's local properties are checked first, followed by its immediate parents, and lastly its distant ancestors.

---

### 2. Expected Viva Questions & Answers

**Q1. What is a Semantic Network?**
**Answer:** Ma'am, a Semantic Network is a technique to represent knowledge as a graph. It uses nodes for concepts and links for relationships. In our code, we store this knowledge as `(Subject, Relation, Object)` triples, like `(bird, can, fly)`.

**Q2. How does inheritance work in your code?**
**Answer:** Ma'am, inheritance works through the `is-a` relation. If we query a property for a "penguin", the algorithm first checks locally. If not found, it follows the `is-a` link to its parent ("bird") and then grandparent ("animal"). It's a bottom-up search.

**Q3. How did you handle exceptions, like penguins not flying?**
**Answer:** Ma'am, we used a specific negative relation `cannot`. The query algorithm always checks for local exceptions (`cannot`) before moving up to the parent class. So, it finds `(penguin, cannot, fly)` locally and returns it, overriding the "can fly" property inherited from the bird class.

**Q4. What is the difference between Semantic Networks (Part 1) and Frames (Exercise 2)?**
**Answer:** Semantic Networks store data in scattered triples. Frames group all properties of a single concept together into one structured dictionary or object. In frames, we use the `ako` (a-kind-of) slot instead of the `is-a` link. Frames are generally more organized.

**Q5. What is Multiple Inheritance and how did you resolve conflicts?**
**Answer:** Ma'am, multiple inheritance is when a node has more than one parent (e.g., a Bat is a Mammal and a Flying Creature). To resolve conflicts if their properties clash, we used Breadth-First Search (BFS) to define an inheritance order. This ensures immediate parents are checked before distant ancestors.

**Q6. What happens if your query function doesn't find a property at all?**
**Answer:** Ma'am, if the algorithm climbs the entire inheritance chain and still doesn't find the requested property or an exception, the loop exhausts and it returns the default string `"unknown"`.

---
*Created by AI for AI401 - Expert Systems Lab preparation.*
