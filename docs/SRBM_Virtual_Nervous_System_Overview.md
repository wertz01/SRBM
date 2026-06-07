# SRBM Virtual Nervous System Overview

This document establishes the foundational conceptual architecture of the Symmetric Rigid Body Maneuvering (SRBM) framework. By decoupling tactical cognition from aerodynamic execution, SRBM provides an airframe-agnostic control topography capable of high-authority, non-linear maneuvering. 

---

## 1. Architectural Mandate

Modern autonomous aviation is traditionally bottlenecked by the tight coupling of guidance logic to platform-specific aerodynamics. If an autonomous policy must constantly calculate physical control allocations, its computational throughput for tactical reasoning drops significantly.

The SRBM paradigm resolves this by mimicking a biological nervous system. It establishes a multi-tiered hierarchy that abstracts physical control surface complexity away from the tactical core, transforming any host platform into a standardized, virtualized 6-DoF rigid body.

---

## 2. Topographical Model

```text
       [ LAYER 3: COGNITION MANIFOLD ]  ← (Motor Cortex)
                      ↓ 
          Idealized Rigid-Body Intent Vector [u_RB]
                      ↓ 
  [ LAYER 2: DETERMINISTIC SAFETY MANIFOLD ]  ← (Vestibular System)
                      ↓ 
         Feasible, Envelope-Compliant Commands
                      ↓ 
    [ LAYER 1: HARDWARE AUTHORIZATION LAYER ]  ← (Spinal Reflex Arc)
                      ↓ 
     High-Rate Actuator Output (20 kHz Loop)
                      ↓ 
             [ PHYSICAL AIRFRAME ]
```

---

## 3. Layer Functionality Breakdown

### Layer 3 — The Cognition Manifold (Motor Cortex)
Layer 3 operates exclusively within the latent tactical intent space. It has zero visibility into control surface topologies, engine metrics, or actuator state spaces. 

Its sole objective is to output geometric, airframe-agnostic motion intent, modeled as a control vector:

$$u_{RB} = [p, q, r, T, B]^T$$

Where:
* $p, q, r$: Demanded body-frame angular rates (roll, pitch, yaw)
* $T$: Normal force / linear thrust demand
* $B$: Dynamic slip / multi-axis intent bias

This mirrors a biological entity deciding *where* to move in 3D space, completely unconcerned with which muscles must contract to achieve the state change.

### Layer 2 — The Deterministic Safety Manifold (Vestibular System)
Layer 2 serves as the system's proprioceptive governor. It intercepts the unconstrained vector $u_{RB}$ from Layer 3 and projects it mathematically onto a bounded, flyable envelope. This safety substrate calculates:
* Structural load thresholds ($G$-limits)
* Dynamic pressure bounds ($q$-dynamics)
* High-alpha aerodynamic feasibility limits

If Layer 3 commands a state transition that would induce structural failure or aerodynamic stall, Layer 2 instantly de-rotates and reshapes the command at the boundary edge before it can exit the manifold.

### Layer 1 — The Hardware Authorization Layer (Spinal Reflex Arc)
Layer 1 is the high-rate (**20 kHz**), deterministic inner loop with exclusive hardware execution authority. It samples high-fidelity IMU data to run a localized moment-allocation solver. 

Taking the optimized, safe command from Layer 2, it dynamically maps the required rigid-body moments across whatever actuators are present on the host airframe (e.g., flaperons, canards, or thrust-vectoring nozzles). This layer acts as a mechanical stabilizer, absorbing environmental turbulence and atmospheric anomalies beneath the threshold of conscious tactical reasoning.

---

## 4. Tactical Implications

By trapping the complex physics of flight within Layers 1 and 2, the tactical AI policy achieves **absolute cognitive focus**. 

Because the underlying airframe is completely virtualized into a clean geometric input, an organization can compile a single tactical policy and deploy it identically across a swarm of highly disparate vehicles—regardless of variations in surface area, weight distribution, or propulsion types.

---

## 5. Mapping to Formal Technical Specifications

This overview serves as the architectural preamble to the primary engineering documents. To implement the mechanics detailed here, reference the following specification modules:

* **Appendix C (Latent Tactical Intent Space):** Defines the mathematical boundaries of the Layer 3 control vector.
* **Section 0.13.4 (Envelope Enforcement Manifold):** Outlines the non-linear projection math governing Layer 2 boundaries.
* **Moment Allocation Solver (Module 4):** Details the 20 kHz optimization loops and control-effectiveness matrix ($B$-matrix) execution for Layer 1.
