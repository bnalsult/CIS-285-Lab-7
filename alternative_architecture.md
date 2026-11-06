# Alternative Software Architecture for CIS 285 Lab 7

## 1. Architectural Overview

This alternative design proposes a layered, model-driven architecture for a UML learning platform focused on class diagrams and activity diagrams. Unlike a simple one-tier or baseline monolithic layout, this model separates the system into distinct responsibilities so that diagram creation, validation, analytics, and persistence remain independent but interoperable.

The architecture is designed around the following principles:

- Model-centric design: diagrams are treated as structured domain artifacts, not just visual drawings.
- Separation of concerns: editing, validation, persistence, and interpretation are independent services.
- Reusability: diagram definitions can be reused across editing, validation, reporting, and export tasks.
- Extensibility: support for additional UML views (use case, sequence, state) can be added without recreating the entire system.

---

## 2. High-Level Structure

### 2.1 Layered View

The system is organized into five primary layers:

1. Presentation Layer
   - Diagram editor canvas
   - Toolbar and property panels
   - Dashboard for assignments and submissions
   - Diagram navigator and validation status

2. Application Layer
   - Diagram orchestration service
   - Class diagram builder
   - Activity diagram builder
   - Validation engine
   - Export service

3. Domain Layer
   - UML entities (Class, Attribute, Method, Relationship, ActivityNode, DecisionPoint)
   - Diagram models and project rules
   - Constraint definitions and grading logic

4. Infrastructure Layer
   - Persistence repository
   - File storage for saved diagrams
   - Metadata indexing
   - Logging and audit records

5. Integration Layer
   - Import/export adapters
   - Optional LMS/assignment connectors
   - Reporting and review interfaces

---

## 3. Structural Components

### 3.1 Presentation Components

#### DiagramWorkspace
Responsible for user interaction with the visual modeling environment. It manages canvas state, selections, drag-and-drop operations, and object editing.

Responsibilities:
- Render class and activity diagram elements
- Handle user gestures and interactions
- Display validation warnings and completion status
- Manage zoom, pan, and focus behavior

#### ToolbarController
Provides access to modeling tools for drawing, connecting, and labeling shapes.

Responsibilities:
- Create new class boxes, activity nodes, and connectors
- Apply diagram-specific templates
- Trigger rules for consistency checks

#### AssignmentPanel
Displays the assignment context, rubric items, and expected UML components.

Responsibilities:
- Show task requirements
- Highlight missing diagram elements
- Surface evaluation feedback

### 3.2 Application Components

#### DiagramService
The main orchestration component for all modeling operations.

Responsibilities:
- Create, open, save, and close diagrams
- Coordinate model creation across class and activity views
- Manage lifecycle for active sessions

#### ClassDiagramEngine
Builds and maintains class diagram structures.

Responsibilities:
- Add entities and relationships
- Validate naming consistency
- Check completeness against lab requirements

#### ActivityDiagramEngine
Builds and maintains activity flows.

Responsibilities:
- Create action nodes, decision nodes, joins, and terminal states
- Sequence execution flow validation
- Detect unreachable or ambiguous workflow paths

#### ValidationEngine
Ensures that diagrams satisfy expected UML conventions and assignment rules.

Responsibilities:
- Detect missing attributes or relationships
- Validate decision logic in activity diagrams
- Check diagram completeness and naming rules
- Produce warnings and completion reports

#### ExportService
Converts diagrams into reusable outputs such as image formats or structured markup.

Responsibilities:
- Export to PNG/SVG or printable formats
- Prepare project snapshots
- Generate review-ready summaries

### 3.3 Domain Components

#### UMLDiagram
A core abstraction representing a diagram as a semantic model rather than only pixels on a canvas.

Key attributes:
- diagramId
- title
- type (ClassDiagram or ActivityDiagram)
- nodes
- edges
- validationState

#### ClassEntity
Represents a domain entity in a class diagram.

Key attributes:
- name
- attributes
- methods
- relationships
- visibility

#### RelationshipEdge
Represents connections between classes or diagram objects.

Key types:
- association
- aggregation
- composition
- inheritance
- dependency

#### ActivityNode
Represents a single step, branch, or terminal point in a process flow.

Key types:
- start
- action
- decision
- merge
- end

#### RuleSet
Defines assignment-specific guidelines and grading constraints.

Responsibilities:
- Identify required elements
- Define allowed relationship types
- Flag ambiguous structures

### 3.4 Infrastructure Components

#### DiagramRepository
Stores and retrieves diagrams and project metadata.

Responsibilities:
- Save user work
- Manage historical revisions
- Load completed or in-progress diagrams

#### ValidationLogStore
Captures validation events and review issues.

Responsibilities:
- Record errors and warnings
- Support instructor feedback
- Retain traceability for corrections

#### FileStorageAdapter
Abstracts storage behind a portable interface for local or cloud-backed files.

Responsibilities:
- Store exports
- Save diagrams in structured formats
- Support versioned project snapshots

---

## 4. Data Flow Architecture

### 4.1 User-to-Diagram Flow

1. User selects a lab scenario or opens an assignment.
2. AssignmentPanel loads the required diagram type and evaluation rules.
3. DiagramWorkspace initializes the drawing canvas for a new or existing model.
4. User adds class or activity elements through ToolbarController.
5. DiagramService updates the active UMLDiagram model.
6. ValidationEngine checks the model against assignment constraints.
7. Resulting issues are displayed in the UI and persisted in the validation log.
8. User corrects or refines the diagram until the model meets expected criteria.

### 4.2 Diagram Persistence Flow

1. DiagramWorkspace emits the current model state.
2. DiagramService serializes the semantic model.
3. DiagramRepository stores the structure and metadata.
4. Model snapshot is indexed for search, recovery, and review.
5. ExportService can later regenerate a visual representation or shareable artifact.

### 4.3 Validation Flow

1. New diagram elements are added to the model.
2. ValidationEngine receives the updated object graph.
3. RuleSet evaluates structural and semantic constraints.
4. Errors and warnings are returned to the UI.
5. Feedback is shown as actionable corrections rather than generic errors.

---

## 5. Alternative Design Pattern Model

### 5.1 Layered Architecture Pattern
This design uses a layered pattern to keep interface concerns away from business logic and persistence. Each layer depends only on the one beneath it, preventing tight coupling between UI logic and model rules.

### 5.2 Model-View-Controller (MVC) Variation
A practical adaptation of MVC is used at the UI level:

- Model: UMLDiagram, ClassEntity, ActivityNode, RelationshipEdge
- View: DiagramWorkspace and visual canvas components
- Controller: DiagramService and ToolbarController

This keeps the user interface responsive while preserving a structured internal representation.

### 5.3 Service-Oriented Domain Services
The application layer uses domain services to encapsulate tasks such as:

- ClassDiagramService
- ActivityDiagramService
- ValidationService
- ReportingService

This creates reusable components that can be tested independently.

### 5.4 Strategy Pattern for Validation
Different validation strategies can be selected depending on diagram type or assignment context.

Examples:
- ClassDiagramValidationStrategy
- ActivityDiagramValidationStrategy
- AssignmentComplianceStrategy

This allows the validation logic to vary by context while preserving a common interface.

### 5.5 Repository Pattern
Repositories isolate model storage and retrieval from business logic. This makes persistence flexible and keeps the domain layer independent from storage details.

### 5.6 Observer Pattern
The UI should update automatically when the diagram model changes. Observers can notify the canvas, validation panel, and assignment overview whenever a diagram is edited.

---

## 6. Alternative Component Interaction Model

```text
User
  -> DiagramWorkspace
     -> DiagramService
        -> ClassDiagramEngine / ActivityDiagramEngine
           -> UMLDiagram
           -> ValidationEngine
              -> RuleSet
                 -> ValidationLogStore
        -> DiagramRepository
        -> ExportService
```

This interaction model shows a coherent flow from user action to domain processing, validation, persistence, and output generation.

---

## 7. Recommended Design for This Lab

For CIS 285 Lab 7, the architecture should remain understandable for teaching and implementation. The most effective alternative is a modular architecture with the following emphasis:

- Frontend editing tools for class and activity diagrams
- Semantic model layer for UML constructs
- Independent validation rules for completeness and correctness
- Repository-backed persistence for saved assignments
- Export and review functions for final deliverables

This differs from a baseline layout because it does not treat the diagram editor as a single page with hard-coded behavior. Instead, it models UML concepts as reusable domain objects and separates concerns between editing, validation, and persistence.

---

## 8. Benefits of This Alternative Architecture

- Easier to extend with other UML views
- Clear separation of diagram logic and presentation logic
- Better support for assignment validation and rubric checking
- More maintainable and testable architecture
- Cleaner handling of data flow from user actions to stored models

---

## 9. Summary

The proposed alternative architecture is a layered, model-driven design that treats UML diagrams as structured, validated artifacts. It supports both class diagrams and activity diagrams through dedicated engines while centralizing validation and persistence. This architecture provides a stronger foundation for student learning, diagram correctness, and future system growth than a simple baseline presentation-first design.
