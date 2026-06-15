# Qiskit v2.x Certification Practice Exam

This practice exam contains 25 multiple-choice questions designed to align precisely with Qiskit v2.x syntax, the IBM Quantum Runtime V2 primitive architecture, and OpenQASM 3 specifications. 

---

## Practice Questions

### 1. Which two operations will result in a SparsePauliOp that represents exactly the operator $-iY$?

A. 
```python
from qiskit.quantum_info import Pauli
p = Pauli('X') @ Pauli('Z')
```

B. 
```python
from qiskit.quantum_info import SparsePauliOp
SparsePauliOp.from_list([("Y", -1j)])
```

C. 
```python
from qiskit.quantum_info import Pauli
p = Pauli('Z') @ Pauli('X')
```

D. 
```python
from qiskit import QuantumCircuit
from qiskit.quantum_info import Pauli
qc = QuantumCircuit(1)
qc.y(0)
Pauli(qc)
```

---

### 2. What is the correct representation of the operator created by the following line of code under Qiskit's little-endian ordering convention?

```python
from qiskit.quantum_info import SparsePauliOp
SparsePauliOp.from_sparse_list([("XYZ", (1, 3, 4), 2.0)], num_qubits=6)
```

A. `SparsePauliOp(['ZXIYII'], coeffs=[2.+0.j])`

B. `SparsePauliOp(['IZYIXI'], coeffs=[2.+0.j])`

C. `SparsePauliOp(['IXIYZE'], coeffs=[2.+0.j])`

D. `SparsePauliOp(['IIXYZI'], coeffs=[2.+0.j])`

---

### 3. Given the code block below, what is the exact analytical probability of observing the state $|1>$ upon running an ideal computational basis measurement?

```python
from qiskit import QuantumCircuit
import numpy as np

qc = QuantumCircuit(1)
qc.ry(np.pi / 3, 0)
qc.rz(np.pi / 2, 0)
```

A. 0.25

B. 0.75

C. 0.5

D. 0.125

---

### 4. Which visualization method should be chosen to visualize a multi-qubit quantum state specifically when you need to highlight continuous phase values by color mapping across computational basis state projections without displaying a full density matrix?

A. `plot_state_city`

B. `plot_state_qsphere`

C. `plot_state_hinton`

D. `plot_bloch_multivector`

---

### 5. What visualization is produced by executing the following snippet on a multi-qubit state, tracking Qiskit's right-to-left string indexing rule?

```python
from qiskit.quantum_info import Statevector
from qiskit.visualization import plot_bloch_multivector

sv = Statevector.from_label('r-')
plot_bloch_multivector(sv)
```

A. Qubit 0 vector points along $+Y$; Qubit 1 vector points along $-Z$

B. Qubit 0 vector points along $-X$; Qubit 1 vector points along $+Y$

C. Qubit 0 vector points along $+X$; Qubit 1 vector points along $-Y$

D. Qubit 0 vector points along $-Z$; Qubit 1 vector points along $+X$

---

### 6. You want to dynamically append measurements to all qubits in your circuit. You have already declared a classical register and want the measurement outcomes to route directly into it without creating an additional, new classical register. Which routine fits this requirement precisely?

A. `qc.measure_all()`

B. `qc.measure_all(add_bits=False)`

C. `qc.measure_active()`

D. `qc.measure()`

---

### 7. When configuring a compilation strategy utilizing the modern pass management framework via `generate_preset_pass_manager`, which parameter option dictates the depth and heuristic computational effort spent optimizing target hardware layouts?

A. `optimization_level`

B. `routing_method`

C. `initial_layout`

D. `approximation_degree`

---

### 8. A user compiles a circuit for an IBM backend using `optimization_level=3`. What structural optimization will they notice regarding consecutive single-qubit gates?

A. All virtual Z gates are transformed into physical RZ microwave pulses.

B. Adjacent single-qubit gates are aggressively combined and parameterized into single target basis gates to minimize errors.

C. The transpiler wraps all operations into un-optimized opaque black-box structures.

D. Every CX gate is systematically replaced with an ECR gate regardless of backend specifications.

---

### 9. Which code snippet correctly implements a parameterized hardware-level control flow loop inside a `QuantumCircuit` instance using standard Qiskit v2.x context-manager syntax?

A. 
```python
with qc.for_loop(range(3)) as i:
    qc.rx(i * theta, i)
```

B. 
```python
for i in range(3):
    qc.rx(i * theta, i)
```

C. 
```python
qc.add_loop(range(3), lambda i: qc.rx(i * theta, i))
```

D. 
```python
with qc.loop(3) as i:
    qc.rx(theta, i)
```

---

### 10. Which two approaches are incorrect when managing job contexts using execution modes in Qiskit Runtime V2 primitives?

A. 
```python
with Session(backend=backend) as session:
    sampler = SamplerV2(mode=backend)
```

B. 
```python
session = Session(backend=backend)
sampler = SamplerV2(mode=session)
```

C. 
```python
with Batch(backend=backend) as batch:
    estimator = EstimatorV2(mode=batch)
```

D. 
```python
sampler = SamplerV2(mode="Batch")
```

---

### 11. What occurs when the `.close()` method is called on an active Qiskit Runtime `Session` or `Batch` object instance?

A. The session immediately stops accepting new jobs, and all currently queued or running jobs within that context are forced to cancel.

B. The session stops accepting new job submissions, but any jobs already submitted within the context are allowed to run to completion.

C. The session remains open indefinitely until the maximum system wall clock limit forces a hard server-side termination.

D. The session context is deleted along with its entire historical job record from the cloud dashboard service database.

---

### 12. How does usage time accumulation differ between Batch mode and Session mode on real IBM Quantum backends?

A. Batch mode limits your usage footprint to active QPU processing time, whereas Session mode tracks the total wall clock time from context opening to closure (including processing pauses).

B. Session mode calculates usage based only on pure gate counts, while Batch mode uses real hardware clock duration metrics.

C. There is no difference; both execution modes charge exclusively for full wall clock time from start to finish.

D. Batch mode charges for the compilation time of circuits, whereas Session mode does not.

---

### 13. Which represents the standard structural layout sequence for executing an experimental workflow with the V2 Estimator primitive?

A. Circuit design -> Primitive instantiation -> Hardware selection -> Execution

B. Backend selection -> Circuit design -> Observable mapping -> Transpilation -> Layout application to observables -> Primitive configuration -> Execution

C. Primitive configuration -> Execution -> Local compilation -> Topology selection

D. Observable mapping -> Execution -> Local transpilation -> Backend selection

---

### 14. You have a parameterized circuit `qct` with two parameters, `alpha` and `beta`. Which code snippet correctly formats the parameter values for a single Primitive Unified Block (PUB) when calling `SamplerV2.run()`?

A. 
```python
pub = (qct, {alpha: [0.1, 0.2], beta: [0.4, 0.5]})
job = sampler.run([pub])
```

B. 
```python
pub = (qct, [0.1, 0.2, 0.4, 0.5])
job = sampler.run([pub])
```

C. 
```python
pub = (qct, [{alpha: 0.1, beta: 0.4}, {alpha: 0.2, beta: 0.5}])
job = sampler.run([pub])
```

D. 
```python
pub = (qct, alpha, beta, [0.1, 0.4])
job = sampler.run([pub])
```

---

### 15. When defining an execution block for `EstimatorV2.run()`, what is the correct structure for a single Primitive Unified Block (PUB) tuple?

A. `(circuit, observables)`

B. `(circuit, observables, parameter_values, precision)`

C. `(circuit, observables, shots)`

D. `(circuit, parameter_values)`

---

### 16. According to the broadcasting rules used by Qiskit Runtime Primitive Unified Blocks (PUBs), what happens if a circuit uses a parameter array of size 5 and an observable array of size 1?

A. The execution fails immediately due to a dimension mismatch error.

B. The single observable is automatically broadcast to match all 5 parameter sets, resulting in 5 expectation values.

C. The execution defaults to a size of 1, discarding the remaining parameter values.

D. The system pads the missing observable slots with identity operators.

---

### 17. You execute a parameterized circuit via SamplerV2 with an array of 4 parameter sets. Assuming your classical register is named 'c', how should you retrieve the measurement counts for the third parameter configuration from the job result object?

A. `result.get_counts(2)`

B. `result[0].data.meas.get_counts()[2]`

C. 
```python
pub_result = result[0]
pub_result.data.c.get_counts(2)
```

D. `result.pub_data[2].counts()`

---

### 18. Which code snippet correctly retrieves a historical list of jobs submitted to an IBM backend named 'ibm_brisbane' under a specific session ID?

A. `service.jobs(backend_name='ibm_brisbane', session_id=my_session_id)`

B. `backend.jobs(session_id=my_session_id)`

C. `Session.from_id(my_session_id).get_all_jobs()`

D. `service.get_backend('ibm_brisbane').history(my_session_id)`

---

### 19. Which line of OpenQASM 3 code correctly declares a fixed-size array of 8 multi-bit registers, where each register is a 4-bit unsigned integer?

A. `uint[4][8] my_array;`

B. `array[uint[4], 8] my_array;`

C. `uint my_array[4][8];`

D. `register uint[4] my_array[8];`

---

### 20. When interacting directly with the IBM Quantum cloud infrastructure via its REST API, which header field must be included to authenticate your requests securely?

A. `Authorization: Bearer <API_TOKEN>`

B. `X-IAM-Key: <KEY>`

C. `Content-Type: application/qasm`

D. `Service-CRN: <CRN_ID>`

---

### 21. What is the native gate configuration behavior when transpiling a circuit for a target backend that natively supports Cross-Resonance (`ECR`) instead of Controlled-NOT (`CX`)?

A. The transpiler will reject the circuit unless you manually replace all CX gates first.

B. Each CX gate is unrolled into an ECR gate combined with local single-qubit rotations.

C. The transpiler converts all operations into software-simulated swap networks.

D. The circuit is executed on the hardware using virtualized CX emulation layers.

---

### 22. Which function provides a straightforward way to dynamically track and print updates on a job's status while it is processing in the IBM Quantum hardware runtime queue?

A. `job.status()`

B. `job.wait_for_final_state()`

C. `job.result(stream=True)`

D. `runtime.monitor(job)`

---

### 23. What happens if you attempt to submit an untranspiled `QuantumCircuit` directly to an IBM Qiskit Runtime V2 primitive execution method?

A. The primitive automatically transpiles the circuit using default optimization settings.

B. The job fails because V2 primitives require circuits to be pre-transpiled to match the backend's native basis gates and physical layout.

C. The primitive routes the circuit to a local simulator instead of the real hardware.

D. The circuit runs normally, but the hardware uses slower fallback emulation pulses.

---

### 24. When using `generate_preset_pass_manager` to target a specific backend, what is the primary benefit of passing the real `backend` object instance instead of just providing a raw list of basis gates?

A. It enables the pass manager to optimize the circuit using real-time dynamic calibration metrics, gate error rates, and the physical coupling map of the device.

B. It automatically authenticates your runtime cloud session with the cloud infrastructure service.

C. It bypasses local compilation and uploads the raw Python code directly to the hardware.

D. It reduces the physical gate execution times on the quantum device.

---

### 25. Which OpenQASM 3 feature allows you to change the execution path of a circuit dynamically based on the outcome of a mid-circuit measurement?

A. Dynamic circuit switch-case or conditional if statements evaluating classical bits.

B. The compiletime verification macro system.

C. The reset instruction.

D. The deferred execution pipeline filter.

---

## Complete Answer Key & Thorough Explanations

### 1. Correct Answers: A, B
* **Why A is correct:** In Qiskit, operator composition `@` evaluates combinations using matrix multiplication sequence logic. Specifically, $X \cdot Z = -iY$. Computing `Pauli('X') @ Pauli('Z')` accurately maps to the Pauli operator string `Y` scaled by a continuous complex phase multiplier equal to $-iY$.
* **Why B is correct:** `SparsePauliOp.from_list([("Y", -1j)])` directly instantiates a sparse matrix string mapping representing the Pauli `Y` multiplied by an explicit scalar complex coefficient of $-1j$, matching $-iY$.
* **Why C is incorrect:** Evaluating `Pauli('Z') @ Pauli('X')` yields the product $Z \cdot X = +iY$, which yields the positive phase $+iY$ instead of $-iY$.
* **Why D is incorrect:** Extracting a `Pauli` operator straight from a `QuantumCircuit` structural layout via `Pauli(qc)` isolates the underlying Clifford operator up to a global phase wrapper. Consequently, global phase scalars like $-i$ are discarded, returning a standard Pauli operator string `Y` with a default positive coefficient of $+1$.

### 2. Correct Answer: B
* **Why B is correct:** Qiskit natively enforces little-endian bit-ordering, meaning qubit index 0 is assigned to the rightmost character in a multi-qubit text mapping string. In this sparse declaration, index 1 is `X`, index 3 is `Y`, and index 4 is `Z`. Mapping this from index 5 down to 0 reads left-to-right as: index 5 (`I`), index 4 (`Z`), index 3 (`Y`), index 2 (`I`), index 1 (`X`), and index 0 (`I`). This perfectly maps to `'IZYIXI'`.
* **Why A, C, and D are incorrect:** These variations result from reversing the little-endian string hierarchy (big-endian interpretations) or miscalculating continuous slicing boundaries instead of explicit individual register index mappings.

### 3. Correct Answer: A
* **Why A is correct:** An initial state $|0
angle$ rotated by an $RY(\pi/3)$ gate yields $\cos(\pi/6)|0
angle + \sin(\pi/6)|1
angle = rac{\sqrt{3}}{2}|0
angle + rac{1}{2}|1
angle$. The subsequent $RZ(\pi/2)$ gate only applies a relative phase shift to the state amplitude ($e^{-i\pi/4}$ and $e^{i\pi/4}$ factors) but preserves the absolute probability magnitude. The measurement probability for observing state $|1
angle$ is exactly $|rac{1}{2}|^2 = 0.25$.
* **Why B, C, and D are incorrect:** Option B ($0.75$) represents the probability of measuring state $|0
angle$. Option C ($0.5$) would occur if an $H$ or $RY(\pi/2)$ gate drove the state completely onto the sphere's equator, which does not match a $\pi/3$ rotation. Option D is a mathematical miscalculation.

### 4. Correct Answer: B
* **Why B is correct:** `plot_state_qsphere` is explicitly customized to display a multi-qubit global state vector as nodes distributed across a sphere, where the size of each node denotes its probability amplitude and its color dynamically maps to its continuous phase angle.
* **Why A is incorrect:** `plot_state_city` plots independent 3D bar graphs split into real and imaginary matrix components rather than using a continuous direct color wheel over a state vector.
* **Why C is incorrect:** `plot_state_hinton` scales box sizes to indicate absolute matrix values and can only differentiate signs using binary contrast colors (black/white), failing to handle continuous complex phases.
* **Why D is incorrect:** `plot_bloch_multivector` decomposes an overall state into separate independent single-qubit Bloch vectors, completely losing all multi-qubit phase entanglement characteristics.

### 5. Correct Answer: B
* **Why B is correct:** Under Qiskit's little-endian convention, the rightmost character of the label represents qubit 0, and the leftmost represents qubit 1. Therefore, in `'r-'`, character `'-'` maps to qubit 0 (pointing to the $-X$ axis on the Bloch multisphere) and `'r'` maps to qubit 1 (representing the Right state, pointing along the $+Y$ axis).
* **Why A, C, and D are incorrect:** These options either reverse the right-to-left qubit index ordering or completely scramble the directional axes mappings for the `'r'`, `'l'`, `'+'`, and `'-'` state symbols.

### 6. Correct Answer: B
* **Why B is correct:** Calling `qc.measure_all(add_bits=False)` sweeps across every single qubit in the circuit and applies a measurement. Setting `add_bits=False` prevents Qiskit from creating its default new classical register (named `"meas"`), forcing it to map outcomes directly into your pre-allocated classical bits instead.
* **Why A is incorrect:** `qc.measure_all()` defaults to `add_bits=True`, which automatically adds an entirely new classical register to the circuit layout, violating the user's constraints.
* **Why C is incorrect:** `qc.measure_active()` targets only non-idle qubits, but its function signature does not accept an `add_bits` flag and it always forces the creation of a brand new classical register named `"measure_active"`.
* **Why D is incorrect:** `qc.measure()` is a basic low-level building instruction that requires you to explicitly pass individual arrays of qubits and bits, rather than acting as a simple automated full-circuit macro.

### 7. Correct Answer: A
* **Why A is correct:** The `optimization_level` parameter (ranging from 0 to 3) in `generate_preset_pass_manager` directly controls the depth, complexity, and algorithmic effort the transpiler uses to simplify structural depth and layout overhead.
* **Why B, C, and D are incorrect:** `routing_method` selects the specific routing algorithm (like stochastic or sabre), `initial_layout` sets a fixed initial physical mapping, and `approximation_degree` adjusts gate approximation thresholds—none of these manage the overall depth configuration of the multi-stage pass structure.

### 8. Correct Answer: B
* **Why B is correct:** At `optimization_level=3`, the transpiler applies aggressive analytical optimization passes that combine consecutive single-qubit gates into single parameterized native basis gates to minimize total gate errors and circuit depth.
* **Why A is incorrect:** Virtual Z gates are executed in software via phase shifts, so they do not require physical microwave pulses.
* **Why C is incorrect:** The transpiler unrolls circuits into explicit native basis gates rather than wrapping them into un-optimized opaque black-box structures.
* **Why D is incorrect:** The transpiler only translates operations into the specific native basis gates supported by the target hardware, rather than forcing a single gate type like `ECR` onto every backend.

### 9. Correct Answer: A
* **Why A is correct:** The syntax `with qc.for_loop(...) as i:` is the correct context manager format used to define dynamic hardware-level loop blocks inside a circuit structure in Qiskit v2.x.
* **Why B is incorrect:** This is a standard Python loop that runs during circuit construction time, which unrolls the gates statically instead of leveraging genuine hardware-level control flow structures.
* **Why C and D are incorrect:** These options use incorrect or deprecated API methods (like `add_loop` or `with qc.loop`), which will cause syntax and execution errors.

### 10. Correct Answers: A, D
* **Why A is an incorrect approach (making it a correct choice for this question):** Passing a physical `backend` object to the primitive's `mode` parameter while inside an active `with Session(backend=backend)` context block causes the primitive to ignore the session context, running the job as an independent execution task instead.
* **Why D is an incorrect approach (making it a correct choice for this question):** The `mode` parameter requires an explicit backend, session, or batch instance object; passing a generic string like `"Batch"` will cause an immediate validation error.
* **Why B and C are valid approaches:** These show correct ways to explicitly define execution modes—either by passing an active session instance directly to the primitive's `mode` parameter or by utilizing the context manager syntax for a batch block.

### 11. Correct Answer: B
* **Why B is correct:** Calling the `.close()` method gracefully shuts down the entry portal for new workloads, preventing the session or batch context from accepting new jobs while allowing any tasks already in the queue to run to completion.
* **Why A, C, and D are incorrect:** These options describe immediate hard cancellations, infinite wait states, or database erasure behaviors that do not match the standard functionality of the `.close()` command.

### 12. Correct Answer: A
* **Why A is correct:** Session mode reserves exclusive access to the QPU to run jobs back-to-back, meaning you are charged for the total wall clock time from context opening to closure (including processing pauses between jobs). Batch mode simply groups jobs in the shared queue without reserving the system, tracking only the active processing time used on the quantum hardware.
* **Why B, C, and D are incorrect:** These options confuse how usage time is tracked, misrepresenting gate counts, uniform wall clock pricing, or local workstation compilation overhead.

### 13. Correct Answer: B
* **Why B is correct:** This sequence accurately outlines the V2 primitive workflow: you must first select a backend and design your circuit, transpile the circuit for that backend, map your observables to match the final physical qubit layout, configure your primitive settings, and then execute the job.
* **Why A, C, and D are incorrect:** These sequences are incorrect because they run operations in the wrong order, such as trying to compile after execution or failing to transpile before applying layout changes to observables.

### 14. Correct Answer: C
* **Why C is correct:** For a circuit with multiple parameters, the parameter values within a single Primitive Unified Block (PUB) must be formatted as a dictionary that maps each `Parameter` object to an array of its corresponding values.
* **Why A, B, and D are incorrect:** These options break the required PUB formatting rules by using invalid dictionary structures, flat lists, or incorrect tuple layouts.

### 15. Correct Answer: B
* **Why B is correct:** An EstimatorV2 PUB tuple follows a flexible four-item structure: `(circuit, observables, parameter_values, precision)`, where the parameter values and target precision fields are optional depending on your circuit setup.
* **Why A, C, and D are incorrect:** These options are incomplete or use parameters like `shots` that are no longer part of individual PUB configurations in the V2 Estimator primitive architecture.

### 16. Correct Answer: B
* **Why B is correct:** Qiskit Runtime V2 primitives follow NumPy-style broadcasting rules. If an execution block contains an observable array of size 1 and a parameter array of size 5, the single observable is automatically scaled up to match all 5 parameter sets, resulting in 5 expectation values.
* **Why A, C, and D are incorrect:** These options describe dimension mismatch errors, data truncation, or generating default identity operators, none of which match the automated broadcasting behavior of the runtime engine.

### 17. Correct Answer: C
* **Why C is correct:** In Qiskit Runtime V2, job results are organized by PUB indices. To get the measurement counts for a specific parameter point, you access the corresponding PUB result, locate your target classical register by name, and then pass the parameter index to its `get_counts()` method.
* **Why A, B, and D are incorrect:** These choices attempt to call methods that do not exist or use obsolete syntax that is not supported by the V2 results API.

### 18. Correct Answer: A
* **Why A is correct:** The `QiskitRuntimeService.jobs()` method provides a straightforward way to search your job history by filtering for specific properties like `backend_name` and `session_id`.
* **Why B, C, and D are incorrect:** These options use incorrect methods on backend or session instances that do not exist in the current Qiskit Runtime API.

### 19. Correct Answer: B
* **Why B is correct:** OpenQASM 3 uses an explicit `array[type, dimensions] name;` syntax to declare fixed-size arrays of registers or variables.
* **Why A, C, and D are incorrect:** These variations use invalid multi-dimensional array layouts, C-style syntax, or incorrect keyword types that violate the OpenQASM 3 language specification.

### 20. Correct Answer: A
* **Why A is correct:** Authenticating direct requests to the IBM Quantum cloud infrastructure REST API endpoints requires an HTTP `Authorization` header containing a valid Bearer token.
* **Why B, C, and D are incorrect:** While parameters like IAM keys, content types, or Cloud Resource Names (CRNs) are used within cloud environments, they do not replace the standard Bearer token header required for secure REST API authentication.

### 21. Correct Answer: B
* **Why B is correct:** Quantum hardware can only execute physical pulses that correspond to its native basis gates. If a backend natively supports `ECR` instead of `CX`, the transpiler automatically unrolls any `CX` gates into an equivalent combination of an `ECR` gate and local single-qubit rotations.
* **Why A, C, and D are incorrect:** These options describe manual gate replacement requirements, routing swap networks, or software emulation layers that do not reflect the standard automated workflow of the transpiler.

### 22. Correct Answer: B
* **Why B is correct:** Calling `job.wait_for_final_state()` blocks your local execution thread and prints progress updates to the console as the job moves through the hardware runtime queue until it reaches a final state.
* **Why A is incorrect:** `job.status()` only checks and returns the job's status at that specific moment, rather than actively listening for or printing updates.
* **Why C and D are incorrect:** These choices use invalid parameters or deprecated utilities like `job_monitor` that are no longer supported in modern versions of Qiskit.

### 23. Correct Answer: B
* **Why B is correct:** Qiskit Runtime V2 primitives strictly separate circuit optimization from execution. To prevent unexpected performance issues and validation overhead, V2 primitives require all input circuits to be pre-transpiled for the target backend, and will fail immediately if given an untranspiled circuit.
* **Why A, C, and D are incorrect:** These options assume that the primitive will automatically transpile the circuit, re-route it to a simulator, or use slower hardware emulation pulses, none of which match the design behavior of the V2 primitives.

### 24. Correct Answer: A
* **Why A is correct:** Providing the real `backend` object gives `generate_preset_pass_manager` access to the system's exact coupling map, calibration records, and gate error metrics, allowing it to optimize gate routing and placement for that specific hardware device.
* **Why B, C, and D are incorrect:** The pass manager is local optimization software and does not handle network authentication, session management, code uploading, or changing physical gate durations on the quantum hardware.

### 25. Correct Answer: A
* **Why A is correct:** OpenQASM 3 supports real-time, hardware-level conditional branching (`if` and `switch` statements), allowing you to change the execution path of a circuit based on mid-circuit measurement outcomes.
* **Why B, C, and D are incorrect:** These choices describe compiletime macros, state initialization routines, or incorrect terms that do not provide real-time conditional branching logic during circuit execution.
