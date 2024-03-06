# Communicating elements of software architecture and design

This notebook is a collection of notes and ideas on communicating elements of
software architecture and design.
It is a work in progress and will be updated throughout 2023 and 2024.

Software architecture is the result of deliberately designing the relationship between
components of a software system.
While a general structure of the relationships can be inferred through reading the
code itself, the architecture of complex software is often difficult to comprehend accurately
and in a reasonable amount of time in this manner.
To enable further development of a software, it is critical to document and communicate
the design intent and architectural elements for both current developers in the future
and new developers joining the project.
In practice, the architecture of a software is often communicated through a combination
of diagrams that each address a different aspect of the holistic design.

This notebook details specific types of diagrams used in the context of communicating software
architecture and design.
Additionally, tools to produce the diagrams are presented along with additional training resources.
Finally, methods for effectively communicating these ideas as part of the project workflow are
proposed.

This is intended to be a community resource, so please engage!
Create a [Discussion](https://github.com/rafmudaf/communicating-design/discussions) in the
repository to talk about a particular concept, or open an
[Issue](https://github.com/rafmudaf/communicating-design/issues) to let me know where I've
missed something. [Pull requests](https://github.com/rafmudaf/communicating-design/pulls)
are welcome, and I will engage with them as quickly as possible.
Lastly, feel free to contact me directly at rafael.mudafort@nrel.gov.

This material will be included as a BSSw Blog Post and an IDEAS HPC Best Practices Seminar soon.
The blog post, slides, and seminar recordings will be linked here when they are published.

```{tableofcontents}
```

# BSSw Blog Post - 2023 BSSw Fellowship: Visually communicating elements of software design

I've been a researcher at the National Renewable Energy Laboratory for seven years, and my role squarely fits into the description of a [research software engineer (RSE)](https://society-rse.org/about/).
In my time at the lab, I've noticed a pattern in funding and staffing cycles where both can be discontinuous or unpredictable resulting in lost momentum and institutional knowledge on software projects.
While this pattern is likely inherent to research itself, RSE's can mitigate these impacts and improve the overall quality of their software by **communicating elements of software design within the development workflow.**
As a [2023 Better Scientific Software Fellow](https://bssw.io/fellows/rafael-mudafort), I've aggregated resources and developed training material to empower RSE's to visually communicate ideas and themes within their software projects, and the results are described here.

Documenting ideas, decisions, and institutional knowledge is a powerful way to mitigate discontinuous momentum during software development efforts.
Early in the development of a software, requirements are identified, and some of them are adopted while others are intentionally rejected.
The form and function of the software starts to take shape.
Capturing these decisions is beneficial to future development efforts considering that the collective knowledge that the development team has in the moment will be different from it's knowledge at a future time.
Given time constraints for software development in the research environment, the process of communicating design decisions can be easily relegated to that elusive "when there's time" moment.
To manage this tendency, I suggest that project teams adopt graphical communication methods to describe conceptual ideas and their implementations using Unified Modeling Language (UML) diagrams and automated tooling.
Narrative content around these diagrams is helpful and encouraged, but the diagrams often speak for themselves.
Once the initial diagrams are in place, future development efforts can build on them to scope and design work while inherently communicating the impact to the entire system.
This article describes UML, and it's role in the development workflow for research software engineers.

## UML, Class Diagrams, and Sequence Diagrams
The [Unified Modeling Language (UML)](https://en.wikipedia.org/wiki/Unified_Modeling_Language) was created in the 1995 and adopted by the Object Management Group, a standards consortium, in 1997.
In essence, UML is a set of graphical notations described by metamodels that enable describing and designing software systems.
UML is particularly relevant to software developed in the object-oriented paradigm, but the methods and notations are broadly relevant to software engineering and systems engineering (see [SysML](https://sysml.org)).
The notations defined in UML can be considered syntax for creating a specific set of diagrams useful in software design and analysis.
While UML defines 14 types of diagrams, the following eight are particularly useful and the first two are described further:
- [Class diagram](https://en.wikipedia.org/wiki/Class_diagram)
- [Sequence diagram](https://en.wikipedia.org/wiki/Sequence_diagram)
- [Package diagram](https://en.wikipedia.org/wiki/Package_diagram)
- [Deployment diagram](https://en.wikipedia.org/wiki/Deployment_diagram)
- [Use case diagram](https://en.wikipedia.org/wiki/Use_case_diagram)
- [State diagram](https://en.wikipedia.org/wiki/State_diagram)
- [Activity diagram](https://en.wikipedia.org/wiki/Activity_diagram)
- [Interaction overview diagram](https://en.wikipedia.org/wiki/Interaction_overview_diagram)

Class diagrams are directly correlated to object-oriented programming.
Attributes and methods on a class can be described with their visibility, argument types, and return type.
Abstract classes and abstract methods are denoted in italics.
Inheritance, aggregation, composition, and association are described with lines connecting classes and specific types of arrows.

::::{grid}
:gutter: 2

:::{grid-item-card} Class
```{mermaid}
classDiagram
    class Class {
        Type attribute1
        Type attribute2
        + public_method(arg1, arg2)
        # protected_method() return_type
        - private_method()
    }
```
:::
:::{grid-item-card} Abstract class
```{mermaid}
classDiagram
    class AbstractClass {
        <<Abstract>>
        Type static_attribute$
        abstract_method()* return_type
    }
```
:::
::::

::::{grid}
:gutter: 3

:::{grid-item-card} Inheritance
```{mermaid}
classDiagram
    BaseClass1 <|-- DerivedFrom1and2
    BaseClass2 <|-- DerivedFrom1and2
    BaseClass2 <|-- DerivedFrom1
```
:::
:::{grid-item-card} Aggregation and Composition
```{mermaid}
classDiagram
    Container o-- AggregationPart
    Container *-- CompositionPart
```
:::
:::{grid-item-card} Association
```{mermaid}
classDiagram
    A -- B
    A --> B
```
:::
::::


Sequence diagrams are broadly applicable to systems when describing algorithms, processes, and procedures.
The metamodel relates participants by passing messages (commands) and data between them.
A rectangle on a participant's line indicated whether a portion is "on" or "off", and boxes encompassing events denote if-statements, loops, and parallel processes.

```{mermaid}
sequenceDiagram
    participant ParticipantA
    participant ParticipantB

    ParticipantA->>+ParticipantB: get_data()
    ParticipantB-->>-ParticipantA: data
    create participant ParticipantC
    ParticipantA->>+ParticipantC: set_data(data)
    ParticipantC->>ParticipantC: sanitize_data(data)
    ParticipantC->>ParticipantC: save_data(data)
    ParticipantC-->>-ParticipantA: void
    alt if this
        ParticipantA->>ParticipantB: b_command()
    else else this
        ParticipantA->>ParticipantC: c_command()
    end
    loop For all data points
        ParticipantA-->>ParticipantB: operation(data)
        ParticipantB-->>ParticipantC: operation(data)
        ParticipantC-->>ParticipantA: operation(data)
    end
```

## Perspective

The UML metamodels provide the syntax to describe a software system with varying levels of fidelity, and it can be tempting to include as much detail as possible.
However, for any relatively complex software, this can be too much information to digest and understand patterns.
I suggest to instead focus on the audience and the specific message to communicate by considering the following questions:
- Who is the intended audience, and what is their level of experience with your software?
- In a few sentences, what specifically are you communicating?
- At what level of fidelity does the content of the message exist in the software?



Identifying and understand the audience is a critical step to any form of communication.
When developing diagrams about a software, I suggest to also spend time identifying the exact message that needs to be communicated.
After the message and target audience are identified, the diagrams can be tailored effectively deliver the message.

For example, the class diagram metamodel provides the syntax to describe a software architecture at levels of fidelity ranging from intra-class to system-level all at once.
However, for any relatively complex software, this can be too much information to digest and understand patterns.

In addition to aspects within a software, these diagrams are useful for describing procedures around a software, such as git-flow and code reviews.


Instead, consider 


::::{grid}
:gutter: 3

:::{grid-item-card} Conceptual
```{mermaid}
classDiagram

    class Floris
    class Farm

    class FlowField {
        u: NDArrayFloat
        v: NDArrayFloat
        w: NDArrayFloat
    }

    class Grid {
        <<abstract>>
        x: NDArrayFloat
        y: NDArrayFloat
        z: NDArrayFloat
    }
    style Grid stroke:#f66,stroke-width:2px,color:#fff

    class WakeModelManager {
        <<interface>>
        combination_model: BaseModel
        deflection_model: BaseModel
        velocity_model: BaseModel
        turbulence_model: BaseModel
    }
    style WakeModelManager stroke:#f66,stroke-width:2px,color:#fff

    class BaseModel {
        <<abstract>>
        dict parameters
        prepare_function()
        function()
    }

    class Solver {
        <<interface>>
        parameters: dict
    }
    style Solver stroke:#f66,stroke-width:2px,color:#fff

    Floris *-- Farm
    Floris *-- FlowField
    Floris *-- Grid
    Floris *-- WakeModelManager
    Floris --> Solver
    WakeModelManager -- BaseModel

    Solver --> Farm
    Solver --> FlowField
    Solver --> Grid
    Solver --> WakeModelManager
```
:::
:::{grid-item-card} Specification
```{mermaid}
classDiagram

  class WakeModelManager {
    combination_function
    deflection_function
    turbulence_function
    velocity_function
    validate_model_strings(instance: attrs.Attribute, value: dict) None
  }
  <<interface>> WakeModelManager
  class GaussVelocityDeficit {
    prepare_function(grid: Grid, flow_field: FlowField) Dict[str, Any]
    function(x_i: np.ndarray,\ny_i: np.ndarray,\nz_i: np.ndarray,\naxial_induction_i: np.ndarray,\ndeflection_field_i: np.ndarray,\nyaw_angle_i: np.ndarray,\nturbulence_intensity_i: np.ndarray,\nct_i: np.ndarray,\nhub_height_i: float,\nrotor_diameter_i: np.ndarray) None
  }
  class GaussVelocityDeflection {
    prepare_function(grid: Grid, flow_field: FlowField) dict[str, Any]
    function(x_i: np.ndarray,\ny_i: np.ndarray,\nyaw_i: np.ndarray,\nturbulence_intensity_i: np.ndarray,\nct_i: np.ndarray,\nrotor_diameter_i: float)
  }
  WakeModelManager -- GaussVelocityDeficit
  WakeModelManager -- GaussVelocityDeflection
```

:::
:::{grid-item-card} Implementation
```{mermaid}
classDiagram
  class BaseClass {
    logger
  }
  class Grid {
    cubature_weights
    grid_resolution : int | Iterable
    n_turbines : int
    n_wind_directions : int
    n_wind_speeds : int
    time_series : bool
    turbine_coordinates
    turbine_diameters
    wind_directions
    wind_speeds
    x_sorted
    x_sorted_inertial_frame
    y_sorted
    y_sorted_inertial_frame
    z_sorted
    z_sorted_inertial_frame
    check_coordinates(instance: attrs.Attribute, value: np.ndarray) None
    grid_resolution_validator(instance: attrs.Attribute, value: int | Iterable) None
    set_grid()* None
    wind_directions_validator(instance: attrs.Attribute, value: NDArrayFloat) None
    wind_speeds_validator(instance: attrs.Attribute, value: NDArrayFloat) None
  }
  <<abstract>> Grid
  class TurbineGrid {
    average_method : str
    sorted_coord_indices
    sorted_indices
    unsorted_indices
    x_center_of_rotation
    y_center_of_rotation
    set_grid() None
  }
  class FromDictMixin {
    as_dict() dict
    from_dict(data: dict)
  }

  FromDictMixin <|-- BaseClass
  BaseClass <|-- Grid
  Grid <|-- TurbineGrid
```
:::
::::




<!-- Show the sequential and full flow solver chart to communicate that this helps to plan new work -->

## Documentation Driven Development

The practice of "test driven development", identifying the criteria of correctness for a particular procedure and writing the tests prior to the implementation, is well understood within the research software communities, and entire ecosystems of software tooling exist to support it.
"Documentation driven development" is less popular, but equally (at least) important for research software, especially given the often discontinuous resources mentioned earlier.
The general idea in documentation driven development is to communicate to a chosen audience about the details of a particular software development effort.
The communication should involve at least the following aspects:
- Design and scope of the work
- Relationship to existing elements of the software including existing implementations and overarching themes
- New themes and design decisions included and excluded
- Updates to the existing documentation relevant to the work

As in test driven development, the "driven" part of documentation driven development is critical.
Ideally, these documents are written before any code, though, in practice, writing it alongside the implementation is acceptable.
A suggested flow using GitHub products is as follows:
1. Describe the scope and design of a software development effort in a GitHub Discussion, and collaborate with colleagues to understand impacts beyond the specific target code
2. After arriving at an acceptable design, create a GitHub Issue that summarizes the Discussion and details the required testing procedures to verify the new code or change
3. Make the code change along with relevant documentation including API docs, usage, function docstrings, and any other relevant material to describe what has been done and how to use it
4. Create a GitHub Pull Request that resolves the open Issue and satisfies the Discussion

## Tools to make it easy

Inaccurate documentation can be worse than no documentation, and manual methods can be inaccurate or missing altogether.
For testing, this conundrum has been solved with continuous integration systems, and I suggest integrating documentation as part of the same workflow.

### mermaid

[Mermaid.js](https://mermaid.js.org) is a JavaScript library for describing diagrams in text and rendering them in web browsers.
Mermaid contains syntax for the eight UML diagrams listed above, as well as additional diagrams not included in UML.
It is well integrated into much of the software development infrastructure including:
- GitHub / GitLab
- VS Code
- Atlassian products
- Slack
- [Many more](https://mermaid.js.org/ecosystem/integrations-community.html)

### Doxygen / graphviz with dot

For C, C++, and Fortran (to some degree) projects, Doxygen is a static code analyzer to create API documentation as well as the following diagrams:
- Class hierarchies
- Include-dependency graphs
- Caller/callee diagrams
- Directory graph (similar to package diagram)

It exports all products into a HTML viewer that can be included as part of any online documentation.
Doxygen itself generates the HTML files and API docs, and it integrates with Graphviz and dot to create the graphs and embeds images into the HTML.

### Pyreverse

For Python projects, pyreverse, part of pylint, is a Python library that analyzes class definitions to create class and package diagrams.
It can output results in PlantUML (.puml), Mermaid (.mmd), HTML, and various image formats, as well as any format supported by Graphviz.

## In summary

Through the BSSw Fellowship, I've had the opportunity to interact with the community to gather ideas on documentation and communication on software design.
In particular, I presented at the NLIT S3C conference in April 2024 ([slides]()) and held an IDEAS/ECP HPC Best Practices Webinar in April 2024 ([video]()).
I've also put together an [online dashboard]() to collect notes, ideas, and examples of good software diagrams that I find.

I see visual communicate as one step toward a pattern language for software design.
We already have plenty of design patterns and syntactic conventions, but we don't currently have an effective language to talk about our systems at a high level and relate them to each other.
I hope to build on this work to continue seeking the pattern language that will unlock true understanding of the systems we create so that we can use it both to create new, more elegant software systems and bring meaningful recognition to the research software engineers who create them.