# Steane-Code-Under-Random-Pauli-Erorr

### The Project: Steane's Code Under Random Pauli Error

Write a Qiskit function that takes the following inputs: (1) A Boolean, $$x\in F_2^n$$; (2) An error probability $$p$$.

The ouput of the function is a quantum circuit that prepares (not neceassarily fault tolerantly) the logical $$|x_L\rangle $$ state in Steane’s code, runs it through a Pauli error channel, with error rate $$p$$ (for each qubits), measures syndromes, applies the recovery operations (if needed), measures the data qubits, and decodes the result.
The success probabilty, is the probabilty that you measure a component of the logical all-zero state at the end. Visualize the dependence of the success probability for various values of $$p$$.

A pauli error channel with error probability $$p$$ means that for each qubit, an $$X$$, $$Y$$, or $$Z$$ error is applied with probability $$p$$ (thus, $$p\leq \frac{1}{3}$$ is necessary). 

#### Note that multiple errors can be applied, as a result, some errors might not be corrected. This is different from standard steane's code that correct one error. 
