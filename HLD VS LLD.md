# High-Level Design (HLD) vs Low-Level Design (LLD)

| Feature                     | High-Level Design (HLD)                             | Low-Level Design (LLD)                                |
|----------------------------|-----------------------------------------------------|--------------------------------------------------------|
| **Purpose**                | Gives an overview of the system architecture        | Describes the detailed internal logic of components    |
| **Focus**                  | System architecture, modules, technologies          | Class diagrams, method-level details, pseudocode       |
| **Granularity**            | Abstract / Macro-level                              | Detailed / Micro-level                                 |
| **Output**                 | Component diagrams, deployment diagrams             | Class diagrams, sequence diagrams, ER diagrams         |
| **Used In**                | Design reviews, architectural planning              | Implementation planning, detailed coding               |
| **Example Questions Answered** | What are the main components? How do they interact? | How is this feature implemented? Which classes/methods?|
| **Technology Stack**       | Specified broadly (e.g., Java + MySQL + Kafka)      | Detailed configurations and usage                      |
| **Dependencies**           | External services, system boundaries                | Internal module dependencies                           |
| **Design Patterns**        | At system or module level (e.g., Microservices, MVC)| At class/method level (e.g., Singleton, Factory)       |

---

## Summary

- **HLD** answers the *"What and Where?"* of the system.
- **LLD** answers the *"How?"* of the components described in HLD.
