# Symmetric Rigid Body Maneuvering (SRBM)

[![License: MIT](https://shields.io)](https://opensource.org)

SRBM is an open, airframe-agnostic architectural framework for autonomous maneuvering systems.

It is **not** a flight controller, **not** a vehicle specification, and **not** a tactical AI model.

SRBM is a **control-virtualization architecture** that separates cognition from physical implementation. It allows autonomous systems to reason in terms of idealized rigid-body motion while deterministic lower layers enforce safety, feasibility, and hardware realization.

The framework was originally motivated by autonomous air combat, but the architecture applies to any vehicle that can be represented as a controllable rigid body, including aircraft, spacecraft, missiles, submarines, and other robotic systems.

---

## Core Thesis

Modern autonomy is often forced to reason in platform-specific implementation details:

- aerodynamic coefficients
- control-surface topology
- actuator dynamics
- structural limits
- propulsion architecture

This tightly couples cognition to a particular vehicle and makes transferring autonomy between platforms difficult.

SRBM introduces a virtualization boundary between cognition and physics.

The cognitive layer issues rigid-body intent.

Deterministic lower layers enforce safety and realize that intent on a specific vehicle.

As a result, autonomy can operate on a stable, geometry-agnostic abstraction rather than the underlying implementation.

---

## Table of Contents

- [Start Here: The SRBM Virtual Nervous System](#start-here-the-srbm-virtual-nervous-system)
- [What Problem SRBM Solves](#what-problem-srbm-solves)
- [Architectural Overview](#architectural-overview)
  - [Layer 3 — Cognition (Motor Cortex)](#layer-3--cognition-motor-cortex)
  - [Layer 2 — Proprioception (Vestibular-System)](#layer-2--proprioception-vestibular-system)
  - [Layer 1 — Reflex Arc (Spinal Loop)](#layer-1--reflex-arc-spinal-loop)
- [Virtualization Boundary](#virtualization-boundary)
- [How to Read This Repository](#how-to-read-this-repository)
- [Scope and Intent](#scope-and-intent)
- [Roadmap](#roadmap)
- [Summary](#summary)

---

# Start Here: The SRBM Virtual Nervous System

For readers new to SRBM, begin with the conceptual overview:

➡️ **[SRBM Virtual Nervous System Overview](docs/SRBM_Virtual_Nervous_System_Overview.md)**

For complete technical details:

📄 **[SRBM Complete Specification (PDF)](docs/SRBM_Complete_Specification.pdf)**

The Virtual Nervous System introduces the architecture through a biological analogy:

## Layer 3 — Cognition (Motor Cortex)

- Tactical intent generation
- Latent doctrine blending
- α/γ doctrine manifold
- Airframe-agnostic motion reasoning

## Layer 2 — Proprioception (Vestibular System)

- Envelope enforcement
- Feasibility projection
- Constraint management
- Deterministic safety guarantees

## Layer 1 — Reflex Arc (Spinal Loop)

- High-rate moment allocation
- Actuator authorization
- Disturbance rejection
- Motion realization

Together these layers transform a physical vehicle into a virtualized rigid-body substrate suitable for machine-native maneuvering.

---

# What Problem SRBM Solves

Many autonomy systems attempt to solve tactical reasoning and physical control simultaneously.

As a result, cognitive policies often become coupled to:

- actuator layouts
- aerodynamic behavior
- propulsion configurations
- platform-specific constraints

This creates a significant AI-to-reality challenge.

SRBM addresses this by separating responsibilities:

| Layer | Responsibility |
|---------|----------------|
| Layer 3 | Determine desired motion |
| Layer 2 | Determine safe motion |
| Layer 1 | Determine how motion is physically produced |

The tactical policy no longer reasons about actuators, control surfaces, or aerodynamic implementation.

Instead, it operates on an idealized rigid-body abstraction.