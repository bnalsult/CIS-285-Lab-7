# Feature Specification: UML Modeling Architecture

**Feature Branch**: `001-uml-modeling-architecture`

**Created**: 2026-11-05

**Status**: Hybrid Consolidated Architecture Draft

**Input**: User description: "A software architecture for CIS 285 Lab 7 focusing on UML modeling, class diagrams, and activity diagrams."

## Purpose

This specification defines the functional and non-functional requirements for a UML modeling tool designed for CIS 285 Lab 7. The design follows a hybrid approach: it preserves the educational clarity of the original requirement set while incorporating a layered, modular architecture that supports maintainability, validation, and future extension.

## User Scenarios & Testing *(mandatory)*

### User Story 1 - Create a class diagram from a domain model (Priority: P1)

A student in CIS 285 Lab 7 needs a consistent way to translate a real-world problem description into a UML class diagram that shows the main entities, their attributes, and the relationships between them.

**Why this priority**: A class diagram is the foundation for understanding the structure of a system and is essential for learners to complete the lab successfully.

**Independent Test**: A learner can define a small set of domain entities, assign their key attributes, and produce a readable class model that explains the structure of the scenario.

**Acceptance Scenarios**:

1. **Given** a course scenario with multiple entities and shared behaviors, **When** the user identifies the core classes, **Then** the system supports a clear representation of each class and the relationships among them.
2. **Given** a defined class, **When** the user adds attributes or responsibilities, **Then** the diagram preserves those details in a way that is easy to review and discuss.

---

### User Story 2 - Model a workflow with an activity diagram (Priority: P1)

A student needs to show how a process moves from one step to the next so that the flow of actions, decisions, and outcomes is visible and easy to interpret.

**Why this priority**: Activity diagrams help learners explain how a workflow behaves over time and are central to understanding process logic in the lab assignment.

**Independent Test**: A learner can describe a workflow, map the major steps, and produce an activity diagram that reflects the sequence and decision points accurately.

**Acceptance Scenarios**:

1. **Given** a process with multiple steps and a decision point, **When** the user adds those steps and branches, **Then** the diagram captures the flow in a logical sequence.
2. **Given** a completed workflow, **When** the user reviews it, **Then** the diagram clearly shows the start, major actions, decision points, and final outcome.

---

### User Story 3 - Review diagram quality and completeness (Priority: P2)

A student or instructor needs a way to confirm that the diagram includes the necessary elements, is clearly labeled, and matches the scenario being modeled.

**Why this priority**: Review and validation help learners catch missing details before submission and improve confidence in their work.

**Independent Test**: A user can evaluate whether the diagram covers the expected entities, relationships, and workflow steps without requiring technical implementation knowledge.

**Acceptance Scenarios**:

1. **Given** a draft diagram, **When** the user reviews it against the assignment requirements, **Then** they can identify missing components and update the model accordingly.
2. **Given** a completed diagram, **When** the user finalizes it, **Then** it remains understandable to peers or instructors who need to assess it.

---

### Edge Cases

- What happens when a user creates a relationship without defining the connected entities?
- How does the system handle duplicate class or action names in the same diagram?
- What happens when a workflow has multiple branches or repeated steps that must be clearly distinguished?
- How does the system handle incomplete or partially defined diagrams during early drafting?
- What happens when an activity diagram contains a decision node without a clear outcome path?

## Requirements *(mandatory)*

### Functional Requirements

- **FR-001**: The system MUST enable users to define and label core entities for a class diagram in a clear and structured manner.
- **FR-002**: The system MUST allow users to add attributes and responsibilities to each class so that the model represents the essential data and behaviors of the scenario.
- **FR-003**: The system MUST support relationships between classes such as association, inheritance, aggregation, composition, and dependency in a visually understandable way.
- **FR-004**: The system MUST support the creation of activity diagrams that represent a sequence of actions, decisions, and outcomes within a workflow.
- **FR-005**: The system MUST allow users to distinguish between normal flow, decision points, merge points, and final conclusions in an activity diagram.
- **FR-006**: The system MUST provide a method for checking diagram completeness so students can confirm the model reflects the assignment requirements.
- **FR-007**: The system MUST allow users to revise or refine a diagram after identifying missing pieces, inconsistent labels, unclear relationships, or invalid workflow logic.
- **FR-008**: The system MUST preserve clear names and labels for all diagram elements so that the model remains understandable to other learners or instructors.
- **FR-009**: The system MUST support both class diagrams and activity diagrams within the same modeling environment without confusion between the two diagram types.
- **FR-010**: The system MUST provide a consistent way to save, reopen, and export a diagram for review or submission.

### Non-Functional Requirements

- **NFR-001**: The system MUST be intuitive enough for students to learn and use within a short lab session without extensive training.
- **NFR-002**: The system MUST provide clear feedback when a diagram is incomplete, ambiguous, or inconsistent.
- **NFR-003**: The system MUST support common classroom scenarios with minimal delay when creating, editing, or validating diagrams.
- **NFR-004**: The system MUST be maintainable by separating modeling logic, validation logic, and user interface concerns.
- **NFR-005**: The system MUST be extensible so additional UML views, validation rules, or reporting features can be added without redesigning the base model.
- **NFR-006**: The system MUST maintain data integrity so that class names, relation types, and activity flow elements remain logically consistent.
- **NFR-007**: The system MUST support review and reproducibility by retaining diagram state, validation results, and revision history.
- **NFR-008**: The system MUST present information in a format suitable for educational use and instructor review.

### Key Entities *(include if feature involves data)*

- **Student**: The learner creating and reviewing diagrams for the lab assignment.
- **Diagram**: A visual representation of a system structure or process, including class or activity information.
- **Class**: A major domain entity that includes its name, attributes, and responsibilities.
- **Relationship**: A connection between classes or workflow elements that expresses dependency, inheritance, association, or composition.
- **Activity Step**: A single action or stage within a process flow.
- **Decision Point**: A location in an activity flow where alternative outcomes may occur.
- **Validation Result**: A record of diagram issues, warnings, or completion status.
- **Assignment**: The lab scenario or exercise that defines required diagram content and evaluation expectations.

## Success Criteria *(mandatory)*

### Measurable Outcomes

- **SC-001**: Students can create a complete class diagram for a typical lab scenario in under 30 minutes.
- **SC-002**: Students can create an understandable activity diagram for a core workflow in under 20 minutes.
- **SC-003**: At least 90% of student-created diagrams include the required entities, relationships, and workflow elements without requiring a major correction cycle.
- **SC-004**: At least 85% of users report that the modeling process improves their understanding of system structure and behavior.
- **SC-005**: Instructors or reviewers can interpret the diagram and complete a meaningful assessment without needing additional clarification from the student.
- **SC-006**: The system identifies and communicates at least 90% of common structural or workflow issues during validation review.

## Assumptions

- The feature is intended for educational use and supports standard UML modeling conventions for coursework.
- Students are expected to create diagrams as part of a structured lab exercise rather than for production system design.
- Diagram quality is assessed by completeness, clarity, and alignment with the assignment scenario.
- The assignment provides the domain context needed to define classes, relationships, and activity flow.
- Basic diagram labeling, editing, validation, and revision are expected to be handled directly by the user without specialized IT tools.
- The architecture will support future extension to additional UML views without requiring a total redesign.
