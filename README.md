# carp-rigidbody

A high-level physical object unification library for the [Carp](https://github.com/carp-lang/Carp) programming language.

This library unifies **`carp-transform`** (where an object is) and **`carp-dynamics`** (how an object moves) into a single, cohesive **`RigidBody`** component. It eliminates the boilerplate of passing around pairs of structs and provides a unified API for the entire physics pipeline.

## Features
- **Unified Data**: Combines Position, Rotation, Scale, Velocity, and Force into one type.
- **Clean Proxy API**: Apply forces, impulses, and step simulations directly on the `RigidBody`.
- **Hardened Invariants**: Leverages the stability and safety of the underlying modular physics stack.
- **Engine Ready**: Designed for use in ECS systems, game scaffolds, and solvers.

## Installation
```clojure
(load "https://github.com/sqrew/carp-rigidbody@master")
```

## Usage
```clojure
(use RigidBody)
(use Vector3)
(use Quaternion)

;; 1. Create a dynamic RigidBody
(let [rb (RigidBody.new (Vector3.init 0.0 10.0 0.0) 
                        (Quaternion.identity) 
                        1.0  ;; Mass
                        0.5  ;; Restitution
                        0.5  ;; Friction
                        0.98 ;; Damping
                        )]
  (do
    ;; 2. Apply a force
    (RigidBody.apply-force! &rb &(Vector3.init 0.0 -9.81 0.0))
    
    ;; 3. Step the simulation
    (RigidBody.step! &rb dt)))
```

## License
MIT
