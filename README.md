# Symmetric Rigid Body Maneuvering (SRBM)

SRBM is an open, airframe‑agnostic architectural framework for autonomous air combat systems. It is not a flight controller, not a vehicle specification, and not a tactical AI model. SRBM is a conceptual operating system for high‑authority, machine‑native maneuvering, designed to separate cognition from aerodynamics and to present any airframe as a clean, idealized 6‑DoF rigid body to an autonomous tactical policy.

## Start Here: The SRBM Virtual Nervous System

For the complete technical engineering details, download the **[SRBM Complete Specification PDF](docs/SRBM_Complete_Specification.pdf)**.

For readers new to SRBM, begin with the conceptual overview:

➡️ **[Read the SRBM Virtual Nervous System Overview](docs/SRBM_Virtual_Nervous_System_Overview.md)**

This document explains the architecture using the virtual nervous system model:

* **Layer 3 — Cognition** (latent‑space tactical intent)
* **Layer 2 — Proprioception** (deterministic envelope enforcement)
* **Layer 1 — Reflex Arc** (20 kHz moment‑allocation loop)

It provides the mental model needed to understand why SRBM separates cognition from aerodynamics and how the three layers interact to produce airframe‑agnostic, high‑authority maneuvering.

## Architectural Overview

The architecture is built around a simple idea: treat the aircraft as a robotic effector platform rather than a traditional aerodynamic vehicle. SRBM defines a three‑layer hierarchy that cleanly isolates tactical reasoning, safety enforcement, and hardware actuation.

### Layer 3 — Cognition Manifold
The top layer produces a normalized rigid‑body intent vector using latent‑space doctrine blending. It operates entirely in a geometric, airframe‑agnostic representation of motion. It does not know what a flaperon, rudder, or thrust‑vectoring nozzle is. It outputs only idealized rigid‑body motion.

### Layer 2 — Deterministic Safety Manifold
This layer projects the cognitive intent onto a feasibility‑safe envelope, ensuring that structural, aerodynamic, and mission constraints are respected. It acts as a proprioceptive safety boundary, reshaping unsafe commands before they ever reach hardware authority.

### Layer 1 — Hardware Authorization Layer
The base layer allocates the resulting rigid‑body moments across the airframe’s multi‑effector control surfaces and propulsion elements. It runs at a high rate (20 kHz) and is the only layer with direct actuator authority. It behaves like a reflex arc, stabilizing and shaping motion beneath conscious tactical reasoning.

## Virtualization Boundary

SRBM assumes a high‑rate inner loop and a slower tactical loop, creating a virtualization boundary that hides aerodynamic complexity and actuator dynamics from the tactical layer. This allows the AI to operate on a stable, geometry‑agnostic representation of motion, independent of:

* Airframe shape
* Control‑surface topology
* Propulsion configuration
* Aerodynamic coefficients

Any platform that provides a control‑effectiveness matrix and actuator limits can host SRBM without modifying the tactical layer.

## Scope and Intent

The framework is intentionally abstract. It does not prescribe:

* Aerodynamic models
* Actuator dynamics
* MPC horizons
* State‑dependent control‑effectiveness matrices
* CFD‑derived coefficients

Those details belong to lower‑level subsystem specifications that vary across platforms, missions, and manufacturers. SRBM defines the interfaces, invariants, and information flow that make machine‑native maneuvering portable and scalable.

This release provides a clear, rigorous, and reusable conceptual foundation for organizations exploring high‑authority autonomous flight. It is offered freely as a seed idea, not tied to any program, contract, or platform. The intent is to inspire new architectures, new airframes, and new ways of thinking about autonomy in contested airspace.

SRBM is a framework for the next generation of autonomous maneuvering systems, built around the principle that an aircraft is simply a robot with an aerodynamic effector shell, and that autonomy should operate on the rigid‑body abstraction rather than the physics beneath it.

---

### Resources
* 📄 **[Download the Full SRBM Specification Document (PDF)](docs/SRBM_Complete_Specification.pdf)**
* 📂 **[Browse the Project Documentation](docs/)**