# Program  Construction

**Programming** is coding an algorithm to a program using a programming language.

**Program construction**  is a methodological process to start from a user’s requirements and end with a working program
as the final product.

## Methodology

### System  Level

- **System Requirements Analysis:**
  Process of identifying and documenting high-level needs and constraints of a system.
- **System Requirements Specification:**
  Detailed description of the functional and non-functional requirements of a system.
- **System Architecture Design:**
  Design of the overall structure and behavior of a system.
- **System Validation:**
  Process of evaluating whether the specifications meet client's requirements.

### Software Level

- **Software Requirements Analysis:**
  Examination and documentation of software-specific needs derived from system requirements.
- **Software Requirements Specification:**
  Detailed description of the functional and non-functional requirements specific to software.
- **Software Architecture Design:**
  Creation of the overall structure and interaction of software components within a system.
- **Software Component/Module Design:**
  Detailed design of individual software components or modules.
- **Program Coding and Testing:**
  Writing code for software components and conducting tests to ensure functionality and quality.
- **Software Deployment and Maintenance:**
  Process of distributing software to users and providing ongoing support and updates.
- **Software Verification:**
  Checking whether the software meets the specified requirements and standards.

## Classification  of  Requirements

|               | Functional Requirements         | Non-functional Requirements           |
|---------------|---------------------------------|---------------------------------------|
| Objective     | Describe what product does      | Describe how product works            |
| End Result    | Define product features         | Define product properties             |
| Focus         | On user requirements            | On user expectations                  |
| Documentation | Captured in Use Cases           | Captured as a quality attribute       |
| Origin Type   | Defined by user (mostly)        | Defined by developers/experts         |
| Testing       | Component, Module, API, UI, ... | Performance, Usability, Security, ... |

### Functional  Requirements

Required functionality or a behavior that a system will exhibit under specific conditions

- **Based on functionality:** A function that a system must be able to perform.
- **Based on behaviour:** The behavioural relationship between input/stimuli and output/response in a system.

### Non-Functional  Requirements

Focuses on the quality attributes, characteristics, and constraints of a system.

#### Performance & Usability

- **interactive:** how fast it responds to certain user actions under a certain workload (responsiveness)
- **non-interactive:** amount of time taken to complete a certain task under a certain workload (speed)

Performance is impacted by the context of execution environment such as Hardware resources (processors, etc.), System
resources (OS type, libraries), Run-time environment (simultaneously active user count, background tasks, etc.).

Jakob Nielsen *(guru of Web page usability)* has suggested 3 main metrics for response time.

- **0.1 seconds**  - the limit after which the system reaction does not seem instantaneous
- **1 second**  - when user will notice the delay, but without interrupted flow of thought
- **10 seconds**  - when user attention is completely lost

#### Security

Most of the security non-functional requirements are mapped to specific functional requirements.

- identification and authentication -> login
- authorized access -> access control matrix
- confidentiality -> encryption
