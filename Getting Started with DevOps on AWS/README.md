# Module 1: Introduction to DevOps

## What is DevOps?
DevOps is the combination of **cultural philosophies, practices, and tools** that enables 
organizations to deliver applications and services at high velocity.

> "Dev" = People and processes that **create** software  
> "Ops" = Teams and processes that **deliver and monitor** software

<img src="https://github.com/gauthamr58/AWS-Zero-to-Hero/blob/main/assets/devops.png" alt="Banner" />

*The infinity loop represents the ongoing collaboration across the software lifecycle.*

---

## The Core Problem
Developers change things quickly, release often, and measure success by the rate of delivery. Operations are driven by maintaining stability of the application. Frequent releases are a cause for concern of the stability and reliability of the application on the supported platforms, especially during high network traffic. 

DevOps brings together formerly siloed roles (development, IT operations, quality engineering, and security) to optimize the productivity of developers and the reliability of operations.

---

## What DevOps Brings Together
- **Culture** — removes barriers, shares end-to-end responsibility
- **Processes** — optimized for speed and quality
- **Tools** — automate repeatable tasks, making releases efficient and reliable

---

## Key Benefits
- Faster delivery of applications and features
- Better collaboration across Dev, Ops, QA, and Security
- Higher reliability and stability
- Ability to quickly respond to business and customer needs

---

## Problems with Traditional Development Practices

Traditional ways of developing software have proven slow and inefficient, and fail to support teams' efforts to quickly deliver stable, high-quality applications. Challenges of **Waterfall development**, **monolithic applications**, **manual processes,** and **siloed** team structures cause bottlenecks and delays.

**Waterfall** is the traditional software development model where you complete each phase fully before moving to the next --- in a strict linear sequence:

<img src= "https://github.com/gauthamr58/AWS-Zero-to-Hero/blob/main/assets/waterfall.png" alt="Banner" />

* Customer sees the product only at the very end   
* If requirements change midway (and they always do), it's   expensive to go back   
* Bugs found late in testing are costly to fix   
* Slow - a full cycle could take months or years

---

**Monolithic application** is a software built as **one single unified unit** where all components are tightly connected and run together.


```text
┌─────────────────────────────┐
│       MONOLITHIC APP        │
│                             │
│  ┌──────────────────────┐   │
│  │    User Interface    │   │
│  ├──────────────────────┤   │
│  │    Business Logic    │   │
│  ├──────────────────────┤   │
│  │    Database Layer    │   │
│  └──────────────────────┘   │
│                             │
│   All in one single unit    │
└─────────────────────────────┘
```
---

**Real world example:**

Think of an e-commerce app --- login, product search, cart, payment, notifications --- all written as **one big application**, deployed as one package.

* * * * *


**The problems it creates:**

-   **Scaling is wasteful** - if only payments are under heavy load, you still have to scale the entire application
-   **One bug can crash everything** - no isolation between components
-   **Hard to update** - changing one small feature requires redeploying the whole app
-   **Slow development** - large codebase, teams stepping on each other
-   **Technology locked** - entire app is tied to one language or framework

---

## 🖥️⚙️ Manual Processes — The Problem

Manual processes throughout the application lifecycle are slow, inconsistent, and error-prone. For example, **manually setting and configuring the infrastructure is time-consuming**. **Manually repeating this process is no guarantee that a step will not be missed**. Another example is telling the developers to **make sure their code is thoroughly tested before pushing it**. Even with the best intentions, this manual process is slow, and does not preclude someone from forgetting a test or two.

---

**Siloed team structure** is when different teams (Dev, Ops, QA, Security) work **separately and independently** with little to no communication between them.

Each team only focuses on their own piece of work and **"throws it over the wall"** to the next team.

```
┌───────────┐     ┌───────────┐     ┌───────────┐     ┌───────────┐
│    DEV    │ →→→ │    QA     │ →→→ │  SECURITY │ →→→ │    OPS    │
│  (Build)  │     │  (Test)   │     │  (Check)  │     │ (Deploy)  │
└───────────┘     └───────────┘     └───────────┘     └───────────┘
  No idea what      No idea what      No idea what     Receives the
  QA/Ops needs      Dev built for     was built or     final product
                    production        tested how        cold
```

* * * * *

**The real world problems it causes:**

-   **Blame culture** --- when something breaks, teams point fingers at each other
-   **Slow delivery** --- work sits in queues waiting to be handed off to the next team
-   **No shared ownership** --- Dev says "it works on my machine", Ops says "not our problem"
-   **Miscommunication** --- each team has different goals, tools, and priorities
-   **Late feedback** --- bugs and issues discovered only when it reaches QA or Ops, expensive to fix by then

---