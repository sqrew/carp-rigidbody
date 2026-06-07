# carp-rigidbody Examples

## 1. Physical Entity Setup
This example shows how a `RigidBody` acts as the single component needed for a physical entity in your world.

```clojure
(load "rigidbody.carp")
(use RigidBody)
(use Vector3)
(use Quaternion)

(defn create-player []
  (let [pos (Vector3.init 0.0 2.0 0.0)
        rot (Quaternion.identity)
        ;; Player: 1.0kg, low bounciness, high friction
        player (RigidBody.new pos rot 1.0 0.2 0.8 0.98)]
    player))
```

## 2. Proxy Accessors
You can interact with the spatial state of the object without reaching into the underlying `transform`.

```clojure
(defn debug-rb [rb]
  (do
    (println* "Current Position: " (Vector3.str (RigidBody.position rb)))
    (println* "Current Velocity: " (Vector3.str @(Body.velocity (RigidBody.body rb))))))
```

## 3. Interaction with Solvers
Because `RigidBody` unifies all data, solvers become much cleaner.

```clojure
(use Solver)

;; Imagine a hypothetical solver call:
(Solver.solve! &rbA &rbB contact)
;; Internally, it can access (RigidBody.transform rbA) and (RigidBody.body rbA) seamlessly.
```
