# Types and usage

Choosing the right type of diagram to communicate an idea first requires identifying
and thoroughly understanding the idea itself.
It is often difficult to communicate all of a software architecture in a single diagram,
so an effective practice is to separate the concepts into well scoped areas and then
choose the best method of communication.
The diagrams described here are not mutually exclusive, and a combination of any of
these should be employed in the overall description of a software.


## What are diagrams and how to make them

Reference the Architecture Diagrams book to describe what a diagram is in the abstract.
Describe the goals of visual representation - why would we want to capture something concrete like computer code as something abstract like a set of boxes connected in various ways?

Refer to the mermaid and software sections.
Present an overview on the existing tools to create diagrams:
- Automatically through things like dot, graphviz; these are typically caller/callee graphs
- Programmatically with tools like mermaid
- Manually with yEd, draw.io, Mural, Miro, etc

# Types of diagrams

Here, I'll list types of diagrams that are commonly used in software architecture and design.
I'll also include suggestions on what types of ideas each can be used to communicate.
This is the primary document in the whole site.


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
