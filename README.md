# Steane-Code-Under-Random-Pauli-Erorr

### The Project: Steane's Code Under Random Pauli Error

Write a Qiskit function that takes the following inputs: (1) A Boolean, $$x\in F_2^n$$; (2) An error probability $$p$$.

The ouput of the function is a quantum circuit that prepares (not neceassarily fault tolerantly) the logical $$|x_L\rangle $$ state in Steane’s code, runs it through a Pauli error channel, with error rate $$p$$ (for each qubits), measures syndromes, applies the recovery operations (if needed), measures the data qubits, and decodes the result.
The success probabilty, is the probabilty that you measure a component of the logical all-zero state at the end. Visualize the dependence of the success probability for various values of $$p$$.

A pauli error channel with error probability $$p$$ means that for each qubit, an $$X$$, $$Y$$, or $$Z$$ error is applied with probability $$p$$ (thus, $$p\leq \frac{1}{3}$$ is necessary). 

#### Note that multiple errors can be applied, as a result, some errors might not be corrected. This is different from standard steane's code that correct one error. 

The codes contain a series of steps. 

### Steane State Preparation. 

The parity-check matrix we used is

$$ H = \begin{pmatrix}
1 & 0 & 0 & 1 & 0 & 1 & 1 \\
0 & 1 & 0 & 1 & 1 & 0 & 1 \\
0 & 0 & 1 & 0 & 1 & 1 & 1 \\
\end{pmatrix} $$

(it is different from conventional parity-check matrix (e.g. (https://errorcorrectionzoo.org/c/steane) ) by some permutations.

The logical $$|0\rangle $$ state is defined as 

$$ |0\rangle_L = \frac{1}{\sqrt{8}} \sum_{Hc=0 (\mathrm{mod} 2)} |c\rangle  $$ 

and the logical $$|1\rangle$$ state is defined as 

$$ |1\rangle_L = \frac{1}{\sqrt{8}} \sum_{Hc=0 (\mathrm{mod} 2)} |c \oplus 1111111\rangle  $$ 

The quantum circuit for $$|0\rangle_L$$ is the following.

<img src="https://github.com/user-attachments/assets/6cdc550c-7ab8-4d77-a473-c349380c3654" width = "400" height = "300" />

### Apply Pauli Error Channel

Errors are randomly applied to each of the 7 physical qubits and the errors can be $$X, Y, Z$$ errors with probability $$p$$. 

### Syndrome Measurements and Error Corrections

These parts are similar to the standard Steane single error correction quantum circuit. I basically borrow the codes from the problem session. 

The code measures $$X$$- and $$Z$$-stabilizers using ancilla qubits, computing syndromes based on the parity-checking matrix $$H$$. $$X$$-stabilizers detect $$Z$$ errors, and $$Z$$-stabilizers detect $$X$$ errors ($$Y=iXZ$$ errors produce both). Recovery operations apply $$X$$ or $$Z$$ gates to correct single-qubit errors based on syndrome values.

### Distribution Analysis

The simulation computes the probability distribution of 7-bit measurement outcomes, separating codewords (from $$p = 0$$) and non-codewords. At $$p = 0$$, only $$|0\rangle_L$$ codewords appear (each $$\sim 0.125$$ probability). As $$p$$ increases, non-codewords emerge due to uncorrectable multi-qubit errors.

The Steane code corrects single-qubit errors, so at low $$p$$, the state remains in the $$|0\rangle_L$$ codespace after correction. At higher $$p$$, multi-qubit errors (weight $$\geq 2$$) cause deviations, producing non-codewords. The probability of $$|0\rangle_L$$ decreases with increasing $$p$$, reflecting the code’s error correction limits.


