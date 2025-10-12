# 🧠 Single-Qubit Gate Operations (Qiskit)

### 🎯 Objective
To explore how single-qubit gates transform quantum states.  
This experiment demonstrates the effect of applying a sequence of gates — `X`, `H`, `S`, `T`, and `RZ` — on a qubit initialized in the |0⟩ state, and then measuring the resulting state probabilities.

---

### 🧩 Program
**File:** `Qiskit_single_qubit_gates.ipynb`

```python
from qiskit import QuantumCircuit, transpile
from qiskit_aer import AerSimulator

# Initialize simulator
sim = AerSimulator()

# Create a single-qubit circuit with one classical bit
qc = QuantumCircuit(1, 1)

# --- Apply sequence of single-qubit gates ---
qc.x(0)        # Pauli-X (NOT gate)
qc.h(0)        # Hadamard (superposition)
qc.s(0)        # Phase gate (π/2)
qc.t(0)        # T gate (π/4)
qc.rz(0.5, 0)  # Z-axis rotation by 0.5 radians

# Measure final state
qc.measure_all()

# Display circuit
print("Quantum Circuit:")
print(qc.draw())

# --- Run simulation ---
compiled = transpile(qc, sim)
result = sim.run(compiled, shots=1024).result()

# --- Display results ---
counts = result.get_counts()
print("\nMeasurement Counts:", counts)
```

---

### 🧠 Concept Recap

| Gate | Symbol | Function |
|------|---------|-----------|
| `X` | Pauli-X | Bit-flip: swaps |0⟩ ↔ |1⟩ |
| `H` | Hadamard | Creates equal superposition |
| `S` | Phase gate | Adds phase of π/2 to |1⟩ |
| `T` | T gate | Adds smaller phase of π/4 |
| `RZ(θ)` | Rotation-Z | Rotates state around Z-axis by θ radians |

---

### 🧭 Procedure
1. Create a quantum circuit with **one qubit and one classical bit**.  
2. Apply gates in the sequence: `X → H → S → T → RZ(0.5)`.  
3. Measure the qubit and simulate using **AerSimulator** with 1024 shots.  
4. Observe and record the output probabilities.  
5. Modify the circuit and analyze how gate order or parameters affect results.

---

### 📊 Expected Output
- The circuit diagram will display the applied gate sequence.  
- Measurement counts (e.g., {'0': 520, '1': 504}) will vary due to quantum probabilistic behavior.  
- Optional: visualize the final state on a **Bloch sphere** using:
  ```python
  from qiskit.visualization import plot_bloch_multivector
  from qiskit.quantum_info import Statevector
  plot_bloch_multivector(Statevector(qc))
  ```

---

### 🧩 Tasks

1. **Change Gate Order**  
   - Swap the order of the `X` and `H` gates.  
   - Run the simulation and observe how the results change.  
   - Explain why gate order affects the final state.

2. **Vary Rotation Angle**  
   - Modify the rotation angle in `qc.rz(θ, 0)` to:  
     - θ = π/4  
     - θ = π/2  
     - θ = π  
   - Compare the measurement counts for each case.

3. **Remove a Gate**  
   - Remove the Hadamard gate (`qc.h(0)`) from the circuit.  
   - Rerun the program and note how the output probabilities differ.
