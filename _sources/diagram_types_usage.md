
# Types and applications

Choosing the right type of diagram to communicate an idea first requires identifying
and thoroughly understanding the idea itself.
It is often difficult to communicate the entirety of a software architecture in a single
diagram, so an effective practice is to separate the concepts into well scoped areas and
choose appropriate methods to communicate each concept.
The diagrams described here are not mutually exclusive, and a combination of these should
be employed in the overall description of a software.

The list of diagrams relevant to software design is extensive, and the practicality
of each type varies with the situation and communication intent.
This list is a subset of common, approachable, and practical diagram types.
All of these are supported by at least one of the diagramming tools described in
[](generators).


## Relational Diagrams

These are the most common and often most practical types of diagrams used in software design.
They allow designers to communicate how various components of a software system interact with
each other at varying levels of fidelity.
In general, blocks representing entities are connected to other blocks with lines that can
contain additional metadata.


(entity_relationship_diagram)=
### Entity-Relationship Diagram

An entity–relationship diagram (ERD, entity-relationship model, or ERM) describes
interrelated things of interest within a domain.
This type of model captures limited low-level details of a system but can describe
extensively the interaction of low-level components.
ERD's are traditionally used to communicate the architecture of relational databases,
but they are also useful to describe the architecture of object oriented software
and are closely related to the [](class_diagram).
and object oriented software systems.
For reference, a simple ERD is shown below.

```{mermaid}
:caption: A basic entity-relationship diagram.

erDiagram
    CAR ||--o{ NAMED-DRIVER : allows
    CAR {
        string registrationNumber
        string make
        string model
    }
    PERSON ||--o{ NAMED-DRIVER : is
    PERSON {
        string firstName
        string lastName
        int age
    }
```

Each entity is depicted as a rectangular box, must have a name, and can optionally be
given attributes.
Entities are typically nouns, and they should correspond to elements of the system
that store data.

```{mermaid}
:caption: An entity-relationship diagram with attributes.

erDiagram
    PERSON
    "PERSON with attributes" {
        string firstName
        string lastName
    }
```

Relationships between entities are typically verbs that connect or operate on entities.
The relationships also contain cardinality information.
A one-to-one relationship means that each entity is tied directly to one other entity.
A one-to-many relationship means that each entity is tied to one or more other entities.
Many-to-many relationships mean that a group of entities are tied to a group of other
entities.
There are a few conventions for indicating relationships in ERDs, and one popular notation
is the crow's foot notation.
When using the [](mermaid), the text-based symbols map to the meaning as given in the
following table. The rendered symbols are also shown in the diagram below.

| Symbol (Left) | Symbol (Right) | Meaning |
| ------------- | -------------- | ------- |
| `\|o`         |  `o\|`         | Zero or one |
| `\|\|`        | `\|\|`         | Exactly one |
| `}o`          | `o{}`          | Zero or many |
| `}\|`         | `\|{`          | One or many |

```{mermaid}
:caption: An entity-relationship diagram with cardinality.

erDiagram
    ZeroOrMany }o--|o ZeroOrOne : ""
    ZeroOrOne o|--|| ExactlyOne : ""
    ExactlyOne ||--|{ OneOrMany : ""
```

**References**:
- [Original publication](https://dl.acm.org/doi/10.1145/320434.320440)
- [Wikipedia](https://en.wikipedia.org/wiki/Entity–relationship_model)
- [Mermaid](https://mermaid.js.org/syntax/entityRelationshipDiagram.html)
- [Miro](https://miro.com/diagramming/er-diagram-many-to-many-relationship/)


(class_diagram)=
### Class Diagram

Class diagrams are used to express the relationship of various organizational components
in a software system.
They are primarily used in the context of object oriented programming (OOP) to communicate
both the internal structure of classes and their relationship to other classes,
and they are related to the [](entity_relationship_diagram).
The Unified Modeling Language (UML) notation system is very closely tied to class diagrams,
and UML provides a powerful ontology for creating them.

Class diagrams contain the following information:
- Class blueprints including encapsulated data and associated methods
- Association between classes
- Inheritance
- Aggregation
- Composition
- Dependency
- Cardinality or multiplicity
See https://www.visual-paradigm.com/guide/uml-unified-modeling-language/uml-class-diagram-tutorial/


<!-- 2. **Association:** An association is a relationship between two or more classes, indicating that objects of one class are somehow related to objects of another class. Associations are often represented as lines connecting the participating classes, and they can have multiplicity (indicating how many objects are involved) and roles (describing the nature of the relationship).
3. **Inheritance/Generalization:** Inheritance is a relationship where one class (the subclass or derived class) inherits attributes and behaviors from another class (the superclass or base class). In a class diagram, inheritance is shown as a solid line with a triangle arrowhead pointing from the subclass to the superclass.
4. **Dependency:** A dependency relationship indicates that one class relies on another class. It is represented by a dashed line with an arrow pointing from the dependent class to the class it depends on. Dependencies can exist between classes due to method parameters, return types, or other interactions.
5. **Association Class:** In some cases, an association between classes may have additional attributes or methods. An association class is a class that is associated with the association itself, and it represents these additional properties or behaviors.
6. **Aggregation:** Aggregation is a specialized form of association that represents a whole-part relationship. It indicates that one class is composed of other classes or objects. It is often represented as a diamond shape on the side of the whole or aggregate class.
7. **Composition:** Composition is a stronger form of aggregation, signifying that the parts of a whole are tightly bound to it and cannot exist independently. It is represented with a filled diamond shape on the side of the whole class.
8. **Multiplicity:** Multiplicity is used to specify how many instances of one class are associated with instances of another class. It is often expressed as a range, such as "1..*" (one or more), "0..1" (zero or one), or specific values like "5." -->



## Flow Charts
https://dev.to/angelotheman/flowchart-wizardry-master-the-art-of-visualizing-algorithms-4e4j

### Data Flow Diagram
https://en.wikipedia.org/wiki/Data-flow_diagram

### Activity Diagram
https://en.wikipedia.org/wiki/Activity_diagram
Activity diagrams are graphical representations of workflows of stepwise activities and
actions with support for choice, iteration and concurrency.
In the Unified Modeling Language, activity diagrams are intended to model both computational
and organizational processes (i.e., workflows), as well as the data flows intersecting with
the related activities.
Although activity diagrams primarily show the overall flow of control, they can also include
elements showing the flow of data between activities through one or more data stores.

https://drawio-app.com/create-uml-activity-diagrams-in-draw-io/


## State Diagram

https://drawio-app.com/blog/uml-state-diagrams-with-draw-io/


## Sequence Diagrams

https://mermaid.js.org/syntax/sequenceDiagram.html
https://drawio-app.com/create-uml-sequence-diagrams-in-draw-io/

## Deployment Diagrams

Describe the infrastructure used to distribute and deploy a software.
AWS and GCP have their own symbols, and UML has a generic symbol set.

https://en.wikipedia.org/wiki/Deployment_diagram
https://www.lucidchart.com/pages/uml-deployment-diagram
https://www.visual-paradigm.com/guide/uml-unified-modeling-language/what-is-deployment-diagram/


# Applications of diagrams

## Elements of software design

- High-level design principles and overarching themes (parti)
- Architecture at various levels of fidelity: top-level (library), mid (integration, function to function), low (within a function)
- Data structures and flow
- Kernel or compute code
- Algorithms; may span various levels of fidelity
- Developer and user workflows; i/o file structures
- Scope of new work within existing projects

## Parti and design abstractions

These diagrams are not fixed. It can be anything that enables communicating the idea that you want to communication.
Be creative! 

## Organizational hierarchies

High-level object diagrams for OOP
- Class diagrams
Function flow for Functional Programming
Module-module interactions
- Component diagrams
Library-library interactions

## Algorithms

Logical steps in words or pseudo code


## Computational cost

Memory access diagrams
CPU/ GPU usage

## Infrastructure processes

Thing like automated testing, release pipelines, and collaborative workflows
- Sequence diagrams
- Deployment diagrams including symbols from AWS and GCP

## User flows

Pipelines for pre and post processing data
Where your software fits into a larger context for a particular topic
