# UML Design Documents for CIS 285 Lab 7

## 1. Design Overview

This document provides the UML design artifacts for the Hybrid Consolidated Architecture. It includes the core structural model for class definitions and the workflow process model for diagram creation and validation.

---

## 2. UML Class Diagram Structure

```mermaid
classDiagram
    class Student {
        +studentId: string
        +name: string
        +createDiagram()
        +reviewDiagram()
    }

    class Assignment {
        +assignmentId: string
        +title: string
        +requirements: string
        +diagramType: string
    }

    class UMLDiagram {
        +diagramId: string
        +title: string
        +status: string
        +save()
        +validate()
        +export()
    }

    class ClassDiagram {
        +entityCount: int
        +relationshipCount: int
        +addClass()
        +addRelationship()
    }

    class ActivityDiagram {
        +nodeCount: int
        +decisionCount: int
        +addAction()
        +addDecision()
    }

    class ClassEntity {
        +name: string
        +attributes: list
        +methods: list
        +visibility: string
    }

    class RelationshipEdge {
        +type: string
        +source: string
        +target: string
        +isValid(): bool
    }

    class ActivityNode {
        +id: string
        +label: string
        +type: string
    }

    class DecisionNode {
        +condition: string
        +outcomes: list
    }

    class ValidationResult {
        +isValid: bool
        +warnings: list
        +errors: list
    }

    Student --> Assignment
    Assignment --> UMLDiagram
    UMLDiagram <|-- ClassDiagram
    UMLDiagram <|-- ActivityDiagram
    ClassDiagram --> ClassEntity
    ClassDiagram --> RelationshipEdge
    ActivityDiagram --> ActivityNode
    ActivityDiagram --> DecisionNode
    UMLDiagram --> ValidationResult
```

### Class Diagram Explanation

The model is designed to represent the core UML building blocks for the lab assignment:

- Student creates or reviews diagrams in the context of an Assignment.
- Assignment defines the problem scenario and expected modeling tasks.
- UMLDiagram is the abstract base type for all diagram types.
- ClassDiagram captures structural entities, attributes, and relationships.
- ActivityDiagram captures process flow, decisions, and action sequencing.
- ValidationResult records whether the diagram satisfies the assignment requirements and notes corrective feedback.

---

## 3. UML Activity Diagram Workflow

```mermaid
flowchart TD
    A[Open assignment] --> B[Choose diagram type]
    B --> C{Diagram type}
    C -->|Class Diagram| D[Create class diagram]
    C -->|Activity Diagram| E[Create activity diagram]

    D --> F[Add class entities]
    F --> G[Add attributes and methods]
    G --> H[Add relationships]
    H --> I[Validate structural model]

    E --> J[Add start node]
    J --> K[Add action steps]
    K --> L[Add decision points and branches]
    L --> M[Validate workflow logic]

    I --> N{Valid?}
    M --> N

    N -->|No| O[Review validation feedback]
    O --> P[Correct diagram]
    P --> B

    N -->|Yes| Q[Save diagram]
    Q --> R[Export or submit for review]
```

### Activity Diagram Explanation

This workflow reflects the practical student process for both UML contexts:

1. The student starts with an assignment.
2. The student chooses the correct diagram type.
3. The student adds the required elements for that diagram.
4. The system validates the structure or workflow.
5. If problems are found, the user revises the diagram.
6. If the model passes validation, the student saves and exports the result.

---

## 4. Design Relationship to Requirements

This design supports the project requirements by ensuring that:

- class diagrams can capture entities, attributes, and relationships
- activity diagrams can capture actions, decisions, and outcomes
- early validation is available to catch incomplete or ambiguous models
- users can revise diagrams before finalizing them
- the system remains maintainable and extensible for additional UML views

---

## 5. Final Design Assessment

The UML class and activity models reflect the hybrid architecture in an implementable way. They align with the lab’s educational goals while preserving a robust software structure for future growth, validation, and review.
