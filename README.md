<p align="center">
  <img src="openots.png" alt="OpenOTS Logo">
</p><h1 align="center">OpenOTS</h1><h3 align="center">Open Object Thinking Standard</h3><p align="center">
  An Open Standard for Structuring, Isolating, and Coordinating AI-Driven Software Projects.
</p><p align="center">
  <a href="#specification-status">
    <img src="https://img.shields.io/badge/Status-Draft-orange" alt="Status: Draft">
  </a>  <a href="#">
    <img src="https://img.shields.io/badge/Type-Open%20Standard-blue" alt="Open Standard">
  </a>  <a href="https://creativecommons.org/licenses/by/4.0/">
    <img src="https://img.shields.io/badge/Documentation-CC%20BY%204.0-green" alt="CC BY 4.0">
  </a>
</p>---

Introduction

What if AI development environments could share a common architecture for building and managing software projects?

OpenOTS (Open Object Thinking Standard) is an open architectural standard designed to establish a unified structure for AI-driven software development.

It defines a standardized way to organize software projects into independent Objects, each with its own implementation workspace, execution context, communication channel, and public interfaces.

OpenOTS introduces a Multi-Agent, Single-Active-Agent Execution Model in which different AI agents may be assigned to different Objects. Each Object can have its own specialized agent, potentially using a different AI model, configuration, or set of capabilities.

However, only one AI agent is permitted to actively execute tasks within an OpenOTS project at any given time. Execution control is transferred between agents through a coordinated handoff mechanism.

Rather than exposing an entire project to an AI agent at once, OpenOTS separates the project into manageable components with clearly defined responsibilities and interaction boundaries.

This allows each agent to focus on its designated Object while preserving a unified project architecture and preventing concurrent AI execution.

Multiple Agents. Independent Contexts. One Active Executor. Standardized Collaboration.

---

The Problem

AI-driven software development introduces a fundamental challenge: AI agents must understand and manage increasingly large software projects while operating within limited context windows and execution environments.

When an AI agent works on an entire project within a single context, several problems can emerge:

- Context consumption caused by unrelated implementation details.
- Unnecessary exposure to other components' internal code.
- Difficulty maintaining clear component responsibilities.
- Increased complexity when managing dependencies.
- Interface changes that can break dependent components.
- Tight coupling between project organization and development environments.
- Difficulty coordinating specialized agents with different capabilities.

OpenOTS addresses these challenges by introducing a standardized object-based architecture that separates implementation, context, communication, and interfaces.

It also establishes a controlled execution model that allows multiple specialized agents to participate in a project without requiring concurrent AI execution.

---

Core Architecture

OpenOTS defines two fundamental Object roles.

1. Manager Object

The Manager Object is the central coordination unit of an OpenOTS project.

It is the only Object responsible for communicating with the user and managing the overall project architecture.

Its responsibilities include:

- Receiving and understanding user requirements.
- Defining the project architecture.
- Decomposing the project into independent software components.
- Creating and maintaining the Dependency Map.
- Defining Worker responsibilities.
- Assigning tasks to Worker Objects.
- Coordinating the overall development process.
- Managing task delegation and execution handoffs.

The Manager may have its own dedicated AI agent, just like any other Object.

2. Worker Object

A Worker Object is an independent development unit responsible for implementing a specific software component.

Its responsibilities include:

- Working within its designated context.
- Implementing its assigned component.
- Operating within its designated workspace.
- Publishing its public APIs through Linker.
- Registering dependencies on external APIs.
- Adapting its implementation when dependent interfaces change.

Each Worker maintains its own implementation and exposes functionality through documented public interfaces.

A Worker may be assigned a dedicated AI agent specialized in its particular responsibilities.

Different Workers may use different AI models, configurations, or capabilities.

Multi-Agent Architecture

OpenOTS supports assigning different AI agents to different Objects.

An Object may have its own dedicated agent, allowing each component to benefit from specialized capabilities and configurations.

For example:

- The Manager may use a general-purpose reasoning model.
- A database Worker may use an agent specialized in database architecture.
- An API Worker may use an agent specialized in backend development.
- A frontend Worker may use an agent specialized in user interface development.

Agent assignment is independent of Object identity.

An Object defines an architectural and execution scope, while its assigned agent defines the AI system responsible for working within that scope.

The standard does not require all Objects to use the same AI model or agent.

Single-Active-Agent Execution Model

Although an OpenOTS project may contain multiple assigned AI agents, only one agent may actively execute tasks within the project at any given time.

This is a fundamental execution constraint of the OpenOTS architecture.

Agents do not execute project tasks concurrently. Instead, execution control is transferred between them through a coordinated handoff mechanism.

A typical execution sequence is:

1. The Manager agent receives the user's requirements.
2. The Manager prepares a task for a Worker.
3. Execution control is transferred to the Worker agent.
4. The Worker agent loads its designated context and reads its incoming Mail.
5. The Worker performs its assigned implementation task.
6. The Worker completes its task and yields execution control.
7. Execution control returns to the Manager or is transferred to another designated Object.

The receiving agent does not automatically inherit the previous agent's entire conversation or working context.

Instead, the receiving Object obtains the information required for its task through its own Context and Mail.

This model allows multiple specialized agents to participate in the same project while maintaining controlled, sequential AI execution.

The host environment is responsible for enforcing the single-active-agent constraint.

---

The Object Model

Every OpenOTS Object follows a unified structural model:

Object/
│
├── Folder/
│
├── Context.txt
│
├── Mail/
│
└── Linker/

The four components define the fundamental structure of an Object.

Folder

The implementation workspace of the Object.

It contains the source code, resources, and implementation files belonging to that Object.

Implementation details should remain isolated from other Objects.

Context

The independent working context of the Object.

It is defined through a file named "Context.txt".

The context provides the AI agent assigned to the Object with the information required to understand and implement the Object's responsibilities.

Each Object maintains its own context, independently of the contexts of other Objects.

Mail

The communication mechanism between Object contexts.

Mail contains structured task documents and notifications directed to a specific Object.

When execution control is transferred to a receiving Object, its assigned agent reads the relevant Mail document to obtain the information required for its task.

Mail is also used by Dependency to notify Objects about changes to APIs they depend on.

Mail therefore provides a standardized communication mechanism between different Objects and their assigned agents.

Linker

The public interface registry of an Object.

It contains the APIs exposed by the Object and their corresponding documentation.

Linker allows other Objects to discover and use functionality without accessing the provider's internal implementation.

Linker follows a fundamental access rule:

Any Object Reading, Only Owner Writing.

- Any Object may read another Object's Linker.
- Only the owning Object may modify its Linker.

---

The Seven Core Principles

OpenOTS is founded on seven architectural principles.

01. Object-Oriented Thinking

A software project must be understood as a collection of independent software components.

Each component has:

- A clearly defined responsibility.
- Its own internal implementation complexity.
- A public API.
- Defined interaction boundaries.

Other components must interact with it through its declared interfaces.

02. Context Isolation

Every Object must maintain an independent working context.

An AI agent should operate within the context of the Object currently being developed.

A Worker should not require the internal implementation details or complete context of other Objects to perform its assigned task.

Each Object's context must remain independent of the contexts of other Objects, regardless of which AI agent is assigned to it.

03. Isolated Folder

Every Object must have a designated implementation workspace.

The implementation files of one Object should remain isolated from those of other Objects.

Other Objects should access functionality through Linker rather than directly accessing internal implementation files.

Actual access restrictions must be enforced by the host development environment.

04. Manager / Worker Objects

An OpenOTS project must contain one Manager Object and may contain multiple Worker Objects.

The Manager coordinates the project and communicates with the user.

Workers independently implement their assigned components.

Each Object may have its own dedicated AI agent.

Different Objects may use different AI models and configurations.

All Objects operate under the Single-Active-Agent Execution Model: only one assigned agent may actively execute tasks within the project at any given time.

05. Mail

Mail provides a standardized document-based communication mechanism between Object contexts.

The Manager creates task documents for Workers.

Workers read their incoming Mail within their own contexts.

Mail also carries Dependency notifications concerning API changes.

Mail additionally supports the information transfer required during execution handoffs between different assigned agents.

06. Linker

Every Object must expose its public APIs through Linker.

Linker contains API definitions and usage documentation.

Its access model is:

Any Object Reading, Only Owner Writing.

07. Dependency

Dependency maintains records of relationships between Objects and the APIs they consume.

When a provider changes an API, Dependency identifies affected consumers and generates notification Mail.

The consuming Workers are responsible for reviewing the updated interface and adapting their implementations.

---

Dependency Management

Dependency is responsible for maintaining API-level relationships between Objects.

Consider the following example:

Worker_A ───── depends on ─────> Worker_B
                                     │
                                     └── Public API

Worker A consumes an API published by Worker B.

The interaction follows this sequence:

1. Worker B publishes its API through Linker.
2. Worker A reads the API documentation.
3. Worker A registers its dependency on that API.
4. Worker B modifies its API.
5. Worker B updates its Linker.
6. Dependency detects the relevant interface change.
7. Dependency generates notification Mail for Worker A.
8. Worker A reads the notification in its own context.
9. Worker A reviews the updated Linker.
10. Worker A adapts its implementation.

Responsibility Boundaries

API Provider:

- Owns and maintains its APIs.
- Updates its Linker.
- Documents interface changes.
- Does not modify consumer implementations.

Dependency:

- Records API dependencies.
- Detects relevant interface changes.
- Identifies affected consumers.
- Generates notification Mail.

API Consumer:

- Registers its dependencies.
- Reviews interface updates.
- Adapts its implementation when necessary.

OpenOTS defines this model without requiring multiple concurrent API versions.

The project is treated as a coordinated system in which affected consumers adapt to the updated interfaces.

---

Platform Interoperability

OpenOTS is designed to be independent of any specific AI development platform.

Its objective is to provide a common architectural structure that different AI Studios can interpret and implement.

An OpenOTS-compatible environment should support the ability to:

- Recognize Manager and Worker Objects.
- Interpret the standardized Object structure.
- Assign AI agents to individual Objects.
- Support different AI models and agent configurations.
- Load independent Object contexts.
- Process Mail documents.
- Discover public APIs through Linker.
- Register and track API dependencies.
- Navigate between Object contexts.
- Transfer execution control between assigned agents.
- Enforce the single-active-agent execution constraint.
- Respect Object implementation boundaries.

OpenOTS does not prescribe:

- A specific AI model.
- A specific programming language.
- A specific development platform.
- A specific AI Studio vendor.
- A specific implementation technology.
- A requirement for all Objects to use the same AI agent.

It defines the organizational and interaction conventions that compatible environments should implement.

Platform-Provided Isolation

OpenOTS relies on the isolation capabilities provided by the host AI development environment.

For example, an AI Studio may provide Trusted Folders or equivalent workspace-level access controls.

The host environment is responsible for enforcing actual file access restrictions.

OpenOTS defines the architectural boundaries that these capabilities must respect.

Logical Object separation and actual security isolation are distinct requirements.

A conforming implementation must not treat context instructions alone as a substitute for enforced workspace access restrictions.

Platform-Provided Execution Control

OpenOTS requires the host environment to enforce exclusive AI execution across the project.

Although different Objects may have different assigned agents, the environment must ensure that no more than one agent actively executes project tasks at any given time.

Execution handoffs must be coordinated so that the previous agent yields execution control before another agent begins executing.

The specific mechanism used to enforce this constraint is left to the host development environment.

---

Project Structure

An OpenOTS project consists of one Manager Object and multiple Worker Objects.

Example:

MyProject/
│
├── Manager/
│   ├── Folder/
│   ├── Context.txt
│   ├── Mail/
│   └── Linker/
│
├── Worker_Auth/
│   ├── Folder/
│   ├── Context.txt
│   ├── Mail/
│   └── Linker/
│
├── Worker_Database/
│   ├── Folder/
│   ├── Context.txt
│   ├── Mail/
│   └── Linker/
│
├── Worker_API/
│   ├── Folder/
│   ├── Context.txt
│   ├── Mail/
│   └── Linker/
│
└── Dependency/
    └── DependencyMap/

Each Object may have an independently assigned AI agent.

Agent assignments and their configurations are managed by the host environment or its OpenOTS implementation.

The Dependency directory represents a possible project-level implementation of dependency management.

Its exact structure and serialization format are subject to further specification.

---

Execution Lifecycle

An OpenOTS project follows a structured development lifecycle.

flowchart TD
    A["User Requirements"] --> B["Manager Object"]
    B --> C["Project Architecture"]
    C --> D["Dependency Map"]
    D --> E["Worker Assignment"]
    E --> F["Task Mail"]
    F --> G["Execution Handoff"]
    G --> H["Assigned Worker Agent"]
    H --> I["Worker Context"]
    I --> J["Component Implementation"]
    J --> K["API Publication"]
    K --> L["Linker"]
    L --> M["Dependency Registration"]
    M --> N["Execution Handoff"]
    N --> O["Manager or Next Worker"]
    O --> P["Project Integration"]

Project Management

1. The Manager agent receives user requirements.
2. The Manager defines the project architecture.
3. The project is decomposed into independent components.
4. A Dependency Map is established.
5. Worker responsibilities are defined.
6. AI agents are assigned to Objects according to their responsibilities and capabilities.

Component Development

1. The Manager prepares task Mail.
2. The current agent yields execution control.
3. Execution control is transferred to the assigned Worker agent.
4. The Worker agent loads its designated context.
5. The Worker reads its incoming Mail.
6. The agent operates within the Worker's designated Folder.
7. The component is implemented.
8. Public APIs are documented and published through Linker.
9. The Worker completes its task and yields execution control.

Component Interaction

1. A Worker discovers required APIs through other Objects' Linkers.
2. It registers dependencies on the consumed APIs.
3. It interacts with other components through their declared interfaces.
4. When another Object needs to perform work, execution control is transferred through a coordinated handoff.

Interface Evolution

1. An API provider modifies its interface.
2. The provider updates its Linker.
3. Dependency identifies affected consumers.
4. Notification Mail is generated.
5. Execution control is transferred to the affected consumer when appropriate.
6. The consumer reviews the updated interface.
7. The consumer adapts its implementation.

Execution Exclusivity

At every point in the execution lifecycle, no more than one AI agent may actively execute tasks within the OpenOTS project.

Different agents may be assigned, configured, and prepared for their respective Objects, but active task execution must remain exclusive.

This constraint ensures controlled execution and prevents concurrent AI agents from independently modifying project components.

---

Specification Status

OpenOTS is currently under development as an open technical standard.

The foundational architecture and seven core principles define the initial direction of the standard.

Further work is required to establish formal and interoperable specifications.

Planned specification areas include:

Specification| Description
Object Model| Formal Object definitions and structural requirements.
Context Model| Context representation and loading conventions.
Mail Protocol| Standardized task and notification document formats.
Linker Protocol| API declaration and documentation formats.
Dependency Protocol| Dependency registration and interface change detection.
Agent Assignment Model| Agent assignment, specialization, and Object-level configuration.
Execution Model| Single-active-agent execution, Object navigation, and execution handoff rules.
Security Model| Workspace isolation and access-control requirements.
Conformance Model| Requirements for platform compatibility and compliance.

The long-term objective is to establish a platform-independent standard that can be implemented across different AI development environments.

---

Contributing

OpenOTS is intended to be an open and community-driven standard.

Technical discussions, architectural reviews, implementation proposals, and contributions are welcome.

Areas of contribution include:

- Core architectural definitions.
- Object structure and schemas.
- Agent assignment and execution models.
- Mail document formats.
- Linker interface specifications.
- Dependency management.
- Security and isolation requirements.
- Execution handoff mechanisms.
- Refere
