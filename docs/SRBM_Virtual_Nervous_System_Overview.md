SRBM Virtual Nervous System Overview
This document provides the conceptual foundation for understanding the three-layer SRBM control architecture. It explains why the system is structured the way it is, how each layer maps to a biological nervous system, and how this separation of responsibilities enables airframe agnostic, high agility autonomous maneuvering.
________________________________________
Purpose of This Document
The formal SRBM specifications define the mathematics, data structures, and control laws that govern autonomous air combat behavior. However, new readers often need a clear mental model before diving into those details.
The SRBM architecture is intentionally designed to mirror the structure of a biological nervous system. This document introduces that model so readers can understand the architectural philosophy behind Layers 1, 2, and 3.
________________________________________
Conceptual Diagram (Placeholder)
[ SRBM Virtual Nervous System Diagram Placeholder ]

Layer 3 — Cognition / Motor Cortex
          ↓ (idealized rigid-body intent)
Layer 2 — Vestibular System / Proprioception
          ↓ (safe, envelope compliant command)
Layer 1 — Spinal Reflex Arc
          ↓ (actuator deflections at 20 kHz)
Airframe — Physical Response
A rendered diagram should be added here in the future.
________________________________________
1. Layer 3 — Cognition / Motor Cortex
Layer 3 operates entirely within the latent tactical intent space defined in Appendix C. It has no awareness of control surfaces, actuators, or aerodynamic mechanisms. Its sole responsibility is to generate an idealized rigid-body motion command:
[ u_{RB} = (p, q, r, T, B) ]
This is equivalent to a human deciding, "I need to pivot my body right now to face the threat." Layer 3 focuses exclusively on tactical reasoning and geometric intent, not on how that intent will be physically realized.
________________________________________
2. Layer 2 — Vestibular System / Proprioception
Layer 2 enforces all physical feasibility constraints. It receives the idealized rigid-body command from Layer 3 and projects it onto the safe, flyable envelope defined by structural limits, dynamic pressure, actuator authority, and mission constraints.
If Layer 3 requests a maneuver that would exceed structural limits or violate aerodynamic feasibility, Layer 2 automatically reshapes the command into a safe version. This mirrors the human vestibular system and brainstem, which prevent the body from performing movements that would cause injury.
________________________________________
3. Layer 1 — Spinal Reflex Arc
Layer 1 runs the high-rate (20 kHz) IMU-driven control loop. It is the only layer with direct authority over actuators. Its role is to convert the safe rigid-body command into coordinated actuator deflections using the control-effectiveness matrix.
This layer behaves like the human spinal cord: it performs rapid, local, reflexive adjustments to maintain stability and achieve the commanded geometry, even in chaotic aerodynamic conditions.
________________________________________
Tactical Consequence — Absolute Cognitive Focus
Because Layers 1 and 2 fully insulate Layer 3 from the mechanics of flight, the tactical AI never spends computational effort on aerodynamics, control allocation, or stability. It operates with complete cognitive freedom, dedicating 100% of its compute to tactical reasoning.
This separation of responsibilities is the core advantage of the SRBM architecture: a clean, hierarchical control stack that mirrors biological systems and enables airframe agnostic, high agility autonomous maneuvering.
________________________________________
Relationship to the Formal Specification
This conceptual model corresponds directly to the formal SRBM documents:
•	Appendix C defines the latent tactical intent space used by Layer 3.
•	Unified Tactical Architecture describes how intent is blended and produced.
•	Envelope Enforcement (Section 0.13.4) defines the Layer 2 safety manifold.
•	Moment Allocation Solver defines the Layer 1 actuator mapping and high-rate control loop.
Readers should use this document as a conceptual on ramp before exploring the mathematical and implementation details in the full specification.

