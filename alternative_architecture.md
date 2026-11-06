# Hybrid Consolidated Architecture for CIS 285 Lab 7

## 1. Architectural Goal

This document consolidates the project’s requirements and software architecture into a hybrid model that preserves the clarity of the requirement specification while adopting the stronger layered, modular architecture recommended during review. The design remains focused on CIS 285 Lab 7 outcomes: UML modeling, class diagrams, activity diagrams, validation of completeness, and educational usability.

The hybrid architecture combines:

- a requirement-driven structure to ensure the system matches the lab goals
- a layered, model-driven software architecture to support maintainability and extensibility
- domain modeling that treats diagrams as structured, validated artifacts rather than simple drawings

---

## 2. Architectural Principles

The system is designed around the following principles:

- Model-centric design: diagrams are treated as semantic structures, not just canvas output.
- Separation of concerns: editing, validation, storage, and export are independent responsibilities.
- Educational clarity: the interface and workflow should remain simple enough for a class assignment.
- Extensibility: additional UML views can be introduced without redesigning the base architecture.
- Validation-first review: users receive immediate feedback on incorrect or incomplete diagram structures.

---

## 3. High-Level Layered Architecture

### 3.1 Presentation Layer

This layer manages the user interaction experience.

Components:
- DiagramWorkspace
- ToolbarController
- AssignmentPanel
- ValidationFeedbackPanel
- ExportDialog

Responsibilities:
- Render class and activity diagrams
- Handle drag-and-drop, selection, editing, and labeling
- Display assignment instructions and rubric expectations
- Show validation issues, warnings, and completion status

### 3.2 Application Layer

This layer contains the orchestration and core business logic for diagram construction and review.

Components:
- DiagramService
- ClassDiagramEngine
- ActivityDiagramEngine
- ValidationEngine
- DiagramExportService
- AssignmentService

Responsibilities:
- Create, open, save, and close diagrams
- Coordinate diagram creation based on assignment type
- Validate class and activity model correctness
- Trigger rule-based checks for assignment requirements
- Export diagrams for review or submission

### 3.3 Domain Layer

This layer contains the UML concepts and core modeling abstractions.

Core Entities:
- UMLDiagram
- ClassDiagram
- ActivityDiagram
- ClassEntity
- Attribute
- Method
- RelationshipEdge
- ActivityNode
- DecisionNode
- ValidationResult
- RuleSet
- Assignment

Responsibilities:
- Represent the semantic structure of class and activity diagrams
- Enforce domain rules for valid UML relationships and workflow logic
- Support assignment-specific validation rules

### 3.4 Infrastructure Layer

This layer provides persistence and technical implementation services.

Components:
- DiagramRepository
- ValidationLogStore
- FileStorageAdapter
- MetadataIndexer
- RevisionHistoryManager

Responsibilities:
- Save diagram state to persistent storage
- Load project history and in-progress work
- Support export and archival snapshots
- Store feedback and validation logs

### 3.5 Integration Layer

This layer connects the system to external capabilities or future expansions.

Components:
- ImportAdapter
- ExportAdapter
- ReviewInterface
- Optional LMSConnector

Responsibilities:
- Import assignments or reference diagrams
- Export to printable or shareable formats
- Support future educational or institutional integrations

---

## 4. Component Decomposition

| Component | Layer | Responsibility |
|---|---|---|
| DiagramWorkspace | Presentation | Manage user editing area and visual structure |
| ToolbarController | Presentation | Launch diagram tools and actions |
| AssignmentPanel | Presentation | Display assignment requirements and rubric cues |
| DiagramService | Application | Coordinate diagram lifecycle and session state |
| ClassDiagramEngine | Application | Build and validate class structures |
| ActivityDiagramEngine | Application | Build and validate workflow structure |
| ValidationEngine | Application | Run completeness and logic checks |
| ExportService | Application | Generate image or document output |
| UMLDiagram | Domain | Core semantic model for all diagrams |
| ClassEntity | Domain | Represent class structure, attributes, and methods |
| RelationshipEdge | Domain | Express associations and inheritance relationships |
| ActivityNode | Domain | Represent action or workflow state |
| RuleSet | Domain | Define diagram expectations and assignment constraints |
| DiagramRepository | Infrastructure | Save and load diagram records |
| ValidationLogStore | Infrastructure | Record warnings, issues, and correction history |
| FileStorageAdapter | Infrastructure | Handle data storage and retrieval |
| LMSConnector | Integration | Connect the tool to external learning platforms |

---

## 5. Data Flow Architecture

### 5.1 User Action Flow

1. User opens an assignment or starts a new diagram.
2. AssignmentPanel loads the required diagram type and restrictions.
3. DiagramWorkspace initializes the canvas and editing tools.
4. The user adds classes, attributes, relationships, actions, decisions, or outcomes.
5. DiagramService updates the underlying UML model.
6. ValidationEngine checks the model against assignment rules.
7. Issues are sent to the validation panel and logged.
8. The user revises the diagram until it is complete and correct.

### 5.2 Persistence Flow

1. DiagramWorkspace emits the current model state.
2. DiagramService serializes the semantic model.
3. DiagramRepository stores the model and metadata.
4. RevisionHistoryManager tracks versions and corrections.
5. ExportService can generate final output for submission or review.

### 5.3 Validation Flow

1. A diagram element is added or changed.
2. ValidationEngine evaluates the model against RuleSet criteria.
3. It checks for:
   - missing class attributes
   - missing relationship definitions
   - invalid activity paths
   - decision points without outcomes
   - duplicate labels or unclear flow
4. ValidationResult is returned to the UI and stored in history.

---

## 6. Design Patterns Used

### 6.1 Layered Architecture Pattern
Divides the system into presentation, application, domain, infrastructure, and integration responsibilities. This keeps the implementation understandable and reduces coupling between UI behavior and domain logic.

### 6.2 Model-View-Controller Variation
The UI layer separates:
- Model: UML diagram objects and relationships
- View: diagram canvas and panels
- Controller: services and interaction handlers

### 6.3 Strategy Pattern for Validation
Validation logic varies by diagram type and assignment context:
- ClassDiagramValidationStrategy
- ActivityDiagramValidationStrategy
- AssignmentComplianceStrategy

This allows rule sets to evolve without rewriting the validation framework.

### 6.4 Repository Pattern
The repository layer isolates business logic from storage logic, enabling simpler persistence management and future changes to storage technology.

### 6.5 Observer Pattern
The UI updates automatically when diagram content changes, so validation feedback, object counts, and relationships remain synchronized.

### 6.6 Factory Pattern (Suggested for Extension)
A factory can create diagram-specific object types and validation services depending on the diagram kind being created.

---

## 7. Hybrid Consolidation Rationale

This hybrid approach is appropriate for CIS 285 Lab 7 because it balances educational clarity and software engineering quality.

The Base Architecture provides:
- direct alignment with the assignment goals
- clear, student-friendly requirements
- measurable outcomes and acceptance criteria

The Alternative Architecture provides:
- serious architectural structure
- modularity and maintainability
- extensibility for future UML features
- a model-driven design that supports validation and persistence

Together, they create a complete design package:
- the specification defines what must be built
- the architecture defines how it should be structured
- the design documents show how the system behaves and represents UML concepts

---

## 8. Benefits of the Hybrid Consolidated Architecture

- Direct alignment with the class assignment and academic requirements
- Clear separation between user-facing behavior and internal logic
- Better support for validation and quality checks
- Easier future extension for additional UML diagram types
- Easier maintenance when updating assignment rules or diagram elements
- Stronger understanding of how modeling tasks map to structured software components

---

## 9. Summary

The Hybrid Consolidated Architecture is the recommended design for CIS 285 Lab 7 because it combines the best of both perspectives: the requirement-driven clarity of the original specification and the engineering quality of the layered alternative architecture. It is suitable for a course environment, but also resilient enough to support future extension and more advanced modeling tasks.
