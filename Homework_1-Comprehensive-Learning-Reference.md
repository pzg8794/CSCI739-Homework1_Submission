# CSCI739 Homework 1 — Comprehensive Learning / Research Reference

**Scope:** Required Problems 1–5 and optional Bonuses A–B, solved from the instructor's pinned Homework 1 source at commit c489b6d29776cb4213d89e0e3d950d26402e7a8a. The source is [Homework 1/main.tex in the archived release](../../CSCI739-Public_Code/CSCI739-Homework_1-Snapshot_c489b6d.zip). The full instructor repository clone, including all Homework 1–5 folders, is in [`../source/`](../source/). This is an AI-assisted study artifact, not a formal submission: the assignment says all submitted work must be written and coded by the student and AI use must be disclosed. Piter must produce his own submitted writing and code and disclose AI assistance as applicable. The separate [expert-assessment version](./Homework_1-Submission-Version.md) presents concise reasoning. [Qiskit verification notebook](./Homework_1-Qiskit-Verification.ipynb) contains executable circuits and saved ideal-simulator results. No submission or instructor feedback has occurred.

**Notation:** In written kets, qubits are ordered left to right as \(\lvert q_0q_1\cdots\rangle\), following the homework. For two qubits the basis order is \((\lvert00\rangle,\lvert01\rangle,\lvert10\rangle,\lvert11\rangle)\). Qiskit labels qubits by index but prints measured classical bits from highest to lowest index; each circuit section maps its count strings explicitly. Amplitudes are complex and probabilities are squared moduli. All circuit claims below are ideal mathematical or Aer-simulator claims, not hardware observations.

**Course grounding:** [QML0 reference](../../Lectures/CSCI739-Lecture_1-QML0-Reference-Summary.md) supplies qubits, bras, measurement, tensors, gates, Bloch sphere and Qiskit order. [QML1 reference](../../Lectures/CSCI739-Lecture_2-QML1-Reference-Summary.md) supplies the distinction between ideal circuits and noisy physical readout. [QML2 reference](../../Lectures/CSCI739-Lecture_3-QML2-Reference-Summary.md) supplies later circuit/fidelity context. The [cross-lecture reference](../../CSCI739-QML0-QML2-Quantum-Foundations-Research-Reference.md) connects these topics. The [course artifact index](../../Communications/2026-09-25_Zoom-Meetings-and-Lecture-Artifact-Index.md) records source coverage. The written homework and QML0 equations control the calculations here; transcript-to-deck mapping is not assumed.

## Problem 1 — Qubit Basics (10 points)

![Equal-superposition amplitude magnitudes and measurement probabilities; the magnitude is squared to obtain probability.](./figures/problem1_amplitude_probability.png)

### A. Exact instructor problem and plain-language task

**Verbatim pinned instructor LaTeX for this numbered problem** (including its summary, figures where present, and every subpart):

~~~tex
\problem{Qubit Basics}{10}
\begin{summary}
This problem introduces the fundamental concept of a single qubit state and how measurement is related to its amplitudes. You will calculate probabilities using Dirac notation and confirm normalization for a specific example.
\end{summary}

Consider a general single-qubit quantum state:
\[
\ket{\psi} = \alpha \ket{0} + \beta \ket{1}, \quad \text{with } \alpha, \beta \in \mathbb{C}, \ |\alpha|^2 + |\beta|^2 = 1.
\]

\begin{enumerate}[label=(\alph*)]
  \item Write the expression for the probability of measuring the qubit in the state $\ket{0}$ and in the state $\ket{1}$, using inner products (bra-ket notation).
  \item Verify that the sum of the two probabilities is always equal to $1$.
  \item For the specific state
  \[
  \ket{\psi} = \tfrac{1}{\sqrt{2}}\ket{0} + \tfrac{1}{\sqrt{2}}\ket{1},
  \]
  calculate explicitly the probability of obtaining $\ket{0}$ and of obtaining $\ket{1}$.
\end{enumerate}
~~~

**Readable problem statement and learning interpretation:**

> Consider a general single-qubit quantum state:
> \[
> \ket{\psi} = \alpha \ket{0} + \beta \ket{1}, \quad \text{with } \alpha, \beta \in \mathbb{C}, \ |\alpha|^2 + |\beta|^2 = 1.
> \]
> (a) Write the expression for the probability of measuring the qubit in the state \(\ket{0}\) and in the state \(\ket{1}\), using inner products (bra-ket notation).
> (b) Verify that the sum of the two probabilities is always equal to \(1\).
> (c) For the specific state
> \[
> \ket{\psi} = \tfrac{1}{\sqrt{2}}\ket{0} + \tfrac{1}{\sqrt{2}}\ket{1},
> \]
> calculate explicitly the probability of obtaining \(\ket{0}\) and of obtaining \(\ket{1}\).

In plain language: project the state onto each computational-basis direction, square the overlap magnitude, check completeness, then evaluate an equal superposition.

### B. What this tests; given and find

This opens the course's mathematical chain: complex amplitudes → orthonormal coordinates → Born-rule probabilities → normalization. It tests linearity, complex conjugation, and the distinction between one sampled result and an ensemble distribution.

**Given:** a normalized ket, complex \(\alpha,\beta\), and orthonormal \(\lvert0\rangle,\lvert1\rangle\). In (c), both amplitudes equal \(1/\sqrt2\). **Find:** two bra-ket probability formulas, proof of their sum, and both numerical probabilities. No Qiskit circuit is requested.

### C. Prerequisites (QML0 §§3.3–3.4)

| Concept | Definition and mathematical form | Physical meaning and why here |
|---|---|---|
| Bra and inner product | \(\langle\psi|=(\alpha^*,\beta^*)\); \(\langle j|\psi\rangle\) is the basis overlap. | A measurement basis defines which component is tested. |
| Orthonormality | \(\langle i|j\rangle=\delta_{ij}\). | A basis bra selects its own amplitude and annihilates the other. |
| Born rule | \(P(j)=|\langle j|\psi\rangle|^2\). | A complex amplitude becomes a real probability only after modulus squaring. |
| Normalization | \(\langle\psi|\psi\rangle=|\alpha|^2+|\beta|^2=1\). | Exhaustive outcomes have total probability one. |

### D. Derivation and full solution

**(a) Starting principle: linearity in the ket and basis orthonormality.**
\[
\begin{aligned}
\langle0|\psi\rangle
&=\langle0|(\alpha|0\rangle+\beta|1\rangle)
=\alpha\langle0|0\rangle+\beta\langle0|1\rangle
=\alpha(1)+\beta(0)=\alpha,\\
\langle1|\psi\rangle
&=\alpha\langle1|0\rangle+\beta\langle1|1\rangle
=\alpha(0)+\beta(1)=\beta.
\end{aligned}
\]
The bra does **not** conjugate the ket coefficient in this expression; conjugation enters when taking the modulus squared (or when forming \(\langle\psi|\)). Thus
\[
\boxed{P(0)=|\langle0|\psi\rangle|^2=\alpha^*\alpha=|\alpha|^2,\qquad
P(1)=|\langle1|\psi\rangle|^2=\beta^*\beta=|\beta|^2.}
\]
This is for measurement in the computational basis.

**(b) Starting principle: the given norm condition.**
\[
P(0)+P(1)=|\alpha|^2+|\beta|^2=1.
\]
The two basis outcomes exhaust this measurement; no third outcome is missing.

**(c) Substitute the specified amplitudes.**
\[
P(0)=\left|\frac1{\sqrt2}\right|^2=\frac12,\qquad
P(1)=\left|\frac1{\sqrt2}\right|^2=\frac12.
\]
The state is \(\lvert+\rangle\). One run yields one classical result; repeated independent preparations approach a 50/50 distribution, without guaranteeing exactly equal finite counts.

### E. Why it works, physical meaning, and independent verification

In column form \(\lvert\psi\rangle=(\alpha,\beta)^T\), \(\langle0|=(1,0)\), and \(\langle1|=(0,1)\), so matrix multiplication independently returns \(\alpha,\beta\). The norm is \((\alpha^*,\beta^*)(\alpha,\beta)^T=1\). For (c), the norm and probability sum are both \(1/2+1/2=1\). A relative phase could alter later interference even though this direct Z-basis probability pair depends only on magnitudes.

### F. Expert checkpoints

| Potential weakness | Why it matters | Correct concept | How our work addresses it |
|---|---|---|---|
| Calling \(\alpha,\beta\) probabilities | They can be complex. | Use \(z^*z\). | Derives overlaps, then modulus squares. |
| Treating \(\langle0|1\rangle\neq0\) | Projection fails. | Orthonormality. | Shows all four basis overlaps. |
| Assuming one shot returns both values | Confuses state with readout. | One projective outcome per shot. | Separates single-shot and ensemble meaning. |
| Omitting the basis | Other bases can give other probabilities. | Measurement basis is part of the claim. | Names computational-basis measurement. |

**Alternative check:** the column-vector calculation and the independent norm check agree with the bra-ket derivation. **Qiskit:** not required for this written problem.

### G. What to remember and later relevance

**Core lesson:** amplitudes are coordinates; probabilities are squared overlap magnitudes. **Equations:** \(\langle j|\psi\rangle=c_j\), \(P(j)=|c_j|^2\), \(\sum_jP(j)=1\). **Intuition:** a basis measurement samples a normalized distribution but need not reveal phase. **Later-course dependency:** tensors in Problem 2, interference in Problem 3, circuit sampling in Problems 4–5, and QML2's distinction between a state and a measurement-derived score.

**What the homework establishes:** the ideal single-qubit Born rule in the specified basis. **What may later be investigated:** how basis choice, finite shots, and physical readout affect a QML or quantum-network observable. This exercise supplies no external system evidence.

### H. Active recall

**Questions:** (1) Why does \(\langle0|\psi\rangle=\alpha\)? (2) Where does complex conjugation enter? (3) Why do these probabilities sum to one? (4) Does a single shot of \(\lvert+\rangle\) return two half-bits?

**Answers:** (1) \(\langle0|0\rangle=1\), \(\langle0|1\rangle=0\). (2) In the bra of a general state and in \(|z|^2=z^*z\). (3) The computational basis is complete and the ket normalized. (4) No: one result, 0 or 1, with equal ideal probabilities.

## Problem 2 — Two-Qubit Systems and CNOT (15 points)

![Exact computational-basis probabilities before CNOT and after each control direction.](./figures/problem2_cnot_probabilities.png)

### A. Exact instructor problem and plain-language task

**Verbatim pinned instructor LaTeX for this numbered problem** (including its summary, figures where present, and every subpart):

~~~tex
\problem{Two-Qubit Systems and CNOT}{15}
\begin{summary}
This problem extends your understanding from single qubits to two-qubit systems. You will define the computational basis states using tensor products, analyze how quantum gates act on these states, and explore the structure of the CNOT operation.
\end{summary}

\begin{enumerate}[label=(\alph*)]
  \item Define each of the four basis states $\ket{00}, \ket{01}, \ket{10}, \ket{11}$ explicitly using tensor product notation between single-qubit states, and then write the vector representation of each of the four basis states.
  \item Consider the two-qubit state
  \[
    \ket{\psi} = \sqrt{\tfrac{1}{10}}\ket{00} + \sqrt{\tfrac{4}{10}}\ket{01} + \sqrt{\tfrac{2}{10}}\ket{10} + \sqrt{\tfrac{3}{10}}\ket{11}.
  \]
  Verify normalization and state the probability of each basis outcome. \textit{Note: In this example the amplitudes are real, but in general they are complex, and the probability is the modulus squared of the amplitude.}
  \item Compute the probability of measuring each basis state after applying a CNOT gate with the left qubit as control and the right as target.
  \item Derive the $4\times 4$ unitary matrix of the flipped-control CNOT (right controls, left is target). \textit{Hint:} track where each basis state maps under this assumption, and create a unitary matrix that would map each basis state to the expected operation.
  \item Prove that the matrix in (d) is unitary.
\end{enumerate}
~~~

**Readable problem statement and learning interpretation:**

> (a) Define each of the four basis states \(\ket{00}, \ket{01}, \ket{10}, \ket{11}\) explicitly using tensor product notation between single-qubit states, and then write the vector representation of each of the four basis states.
>
> (b) Consider the two-qubit state
> \[
> \ket{\psi}=\sqrt{\tfrac{1}{10}}\ket{00}+\sqrt{\tfrac{4}{10}}\ket{01}+\sqrt{\tfrac{2}{10}}\ket{10}+\sqrt{\tfrac{3}{10}}\ket{11}.
> \]
> Verify normalization and state the probability of each basis outcome. *Note: In this example the amplitudes are real, but in general they are complex, and the probability is the modulus squared of the amplitude.*
>
> (c) Compute the probability of measuring each basis state after applying a CNOT gate with the left qubit as control and the right as target.
>
> (d) Derive the \(4\times4\) unitary matrix of the flipped-control CNOT (right controls, left is target). *Hint:* track where each basis state maps under this assumption, and create a unitary matrix that would map each basis state to the expected operation.
>
> (e) Prove that the matrix in (d) is unitary.

In plain language: build the product basis, apply the Born rule to a four-component state, permute its amplitudes with one CNOT orientation, then derive and verify the other orientation's matrix.

### B. What this tests; given and find

Problem 1's two-dimensional space becomes \(\mathbb C^2\otimes\mathbb C^2\cong\mathbb C^4\). The skills are Kronecker products, basis indexing, linear gate action, amplitude bookkeeping, and adjoint-based unitarity. Physically, CNOT is a conditional bit flip, not a measurement.

**Given:** \(|0\rangle=(1,0)^T\), \(|1\rangle=(0,1)^T\); the four amplitudes in (b); computational-basis order \((00,01,10,11)\); left control/right target in (c), reversed in (d–e). **Find:** four vectors, four original and post-CNOT probabilities, flipped-control matrix, and \(U^\dagger U=I\).

### C. Prerequisites (QML0 §§3.4–3.5 and §5)

| Concept | Definition and mathematical form | Physical meaning and why here |
|---|---|---|
| Tensor product | \((a,b)^T\otimes(c,d)^T=(ac,ad,bc,bd)^T\). | A joint basis labels both qubits in a fixed order. |
| Multi-outcome Born rule | \(P(x)=|\langle x|\psi\rangle|^2\). | Each four-component amplitude sets one Z-basis probability. |
| Controlled X | \(\mathrm{CNOT}_{L\to R}|a b\rangle=|a,b\oplus a\rangle\). | The target flips only when its named control is 1. |
| Unitary matrix | \(U^\dagger U=I\). | Ideal gate evolution preserves norms and inner products. |

### D. Derivation and full solution

**(a) Basis construction.** The right factor varies fastest in the declared column order:
\[
\begin{aligned}
|00\rangle&=|0\rangle\otimes|0\rangle=(1,0,0,0)^T,\\
|01\rangle&=|0\rangle\otimes|1\rangle=(0,1,0,0)^T,\\
|10\rangle&=|1\rangle\otimes|0\rangle=(0,0,1,0)^T,\\
|11\rangle&=|1\rangle\otimes|1\rangle=(0,0,0,1)^T.
\end{aligned}
\]
Each is unit length and orthogonal to the other three because single-qubit factors are orthonormal.

**(b) Normalization and Born probabilities.**
\[
\langle\psi|\psi\rangle=\frac1{10}+\frac4{10}+\frac2{10}+\frac3{10}=1,\qquad
(P_{00},P_{01},P_{10},P_{11})=(0.1,0.4,0.2,0.3).
\]
The positive real amplitudes make squaring simple here; a complex coefficient would require its modulus squared.

**(c) Left-control CNOT.** The basis map is \(00\mapsto00,\ 01\mapsto01,\ 10\mapsto11,\ 11\mapsto10\), so
\[
\mathrm{CNOT}_{L\to R}|\psi\rangle
=\sqrt{\tfrac1{10}}|00\rangle+\sqrt{\tfrac4{10}}|01\rangle
+\sqrt{\tfrac3{10}}|10\rangle+\sqrt{\tfrac2{10}}|11\rangle.
\]
Thus \(\boxed{(P'_{00},P'_{01},P'_{10},P'_{11})=(0.1,0.4,0.3,0.2)}\). This gate permutes basis amplitudes; it does not square and add them until measurement.

**(d) Right-control CNOT.** Its rule is \(|a b\rangle\mapsto|a\oplus b,b\rangle\). Therefore \(00\mapsto00,\ 01\mapsto11,\ 10\mapsto10,\ 11\mapsto01\). A matrix column is the output vector of the corresponding input basis state:
\[
\boxed{U_{R\to L}=
\begin{pmatrix}
1&0&0&0\\
0&0&0&1\\
0&0&1&0\\
0&1&0&0
\end{pmatrix}.}
\]
In contrast with (c), this orientation swaps the \(01\) and \(11\) columns/states.

**(e) Unitarity.** The matrix is real symmetric, so \(U^\dagger=U^T=U\). Its action swaps \(01\leftrightarrow11\) and fixes \(00,10\), so applying it twice fixes every basis vector: \(U^2=I_4\). Hence \(U^\dagger U=U^2=I_4\), and also \(UU^\dagger=I_4\). Equivalently, its columns are distinct orthonormal standard basis vectors. Both checks establish unitarity.

### E. Why it works, physical meaning, and independent verification

The tensor product tracks which label belongs to each qubit. A CNOT is a reversible conditional permutation of computational basis states, so each amplitude moves to exactly one output basis state, retaining its complex value. Reversibility explains both \(U^{-1}=U\) and unitarity here. As independent checks: the post-(c) probabilities still sum to \(0.1+0.4+0.3+0.2=1\); \(U_{R\to L}(0,1,0,0)^T=(0,0,0,1)^T\); \(U_{R\to L}(0,0,0,1)^T=(0,1,0,0)^T\); and all columns have unit norm and zero mutual overlaps. These are checks on distinct parts of the derivation.

### F. Expert checkpoints

| Potential weakness | Why it matters | Correct concept | How our work addresses it |
|---|---|---|---|
| Changing the \((00,01,10,11)\) order midway | Matrix columns and probabilities would be misassigned. | Fixed tensor-basis order. | States every vector and mapping explicitly. |
| Swapping the wrong pair under CNOT | Control direction changes the operation. | Evaluate the named control bit. | Lists both direction-specific maps. |
| Squaring before applying the gate | This loses phase information for general states. | Apply the linear unitary to amplitudes first. | Writes the transformed ket before probabilities. |
| Treating norm preservation of one example as a proof of unitarity | One vector cannot establish a matrix identity. | \(U^\dagger U=I\) for all inputs. | Proves \(U^2=I\) and column orthonormality. |

**Alternative check:** multiplying the displayed matrix by each of the four standard basis columns reproduces the stated map. **Qiskit:** no implementation requested for Problem 2.

### G. What to remember and later relevance

**Core lesson:** two qubits have four ordered amplitudes, and a controlled gate acts on the named control/target wires. **Equations:** \((A\otimes B)(|a\rangle\otimes|b\rangle)=A|a\rangle\otimes B|b\rangle\); \(\mathrm{CNOT}_{L\to R}|ab\rangle=|a,b\oplus a\rangle\); \(U^\dagger U=I\). **Intuition:** conditional reversible gates redistribute amplitudes, while measurement samples squared magnitudes. **Later-course dependency:** circuit construction in Problem 4 and reversible arithmetic in Problem 5.

**What the homework establishes:** the ideal two-qubit basis and two CNOT orientations. **What may later be investigated:** how hardware connectivity and native gate direction affect a physical implementation (QML1), or how a QML circuit search encodes legal gate actions (QML2). This calculation is not evidence about a separate quantum network.

### H. Active recall

**Questions:** (1) Which factor varies fastest in the declared two-qubit vector order? (2) Which states does left-control CNOT exchange? (3) Which states does right-control CNOT exchange? (4) Why is the displayed right-control matrix unitary? (5) Why act on amplitudes before squaring?

**Answers:** (1) The right qubit. (2) \(10\leftrightarrow11\). (3) \(01\leftrightarrow11\). (4) Its columns are orthonormal and \(U^\dagger U=U^2=I\). (5) Quantum evolution is linear and can later interfere; probabilities are assigned at measurement.

## Problem 3 — The Bloch Sphere and Single-Qubit Gates (20 points)

![Bloch-sphere positions in the sequence |0>, H|0>=|+>, H²|0>=|0>.](./figures/problem3_hadamard_bloch.png)

### A. Exact instructor problem and plain-language task

**Verbatim pinned instructor LaTeX for this numbered problem** (including its summary, figures where present, and every subpart):

~~~tex
\problem{The Bloch Sphere and Single-Qubit Gates}{20}
\begin{summary}
This problem develops your understanding of the Bloch sphere representation of a qubit and how single-qubit gates act on quantum states. You will translate between amplitude form and Bloch sphere parameters, analyze the action of common gates, and explore interference effects through repeated Hadamard operations.
\end{summary}

\begin{enumerate}[label=(\alph*)]
  \item Any single-qubit state can be written as
  \[
    \ket{\psi} = \cos\!\left(\tfrac{\theta}{2}\right)\ket{0} + e^{i\phi}\sin\!\left(\tfrac{\theta}{2}\right)\ket{1},
  \]
  where $\theta\in[0,\pi]$, $\phi\in[0,2\pi)$.
  Derive $\theta$ and $\phi$ in terms of amplitudes $\alpha,\beta$ for $\ket{\psi}=\alpha\ket{0}+\beta\ket{1}$. State $(\theta,\phi)$ for $\ket{0}$ and $\ket{1}$.

  \begin{center}
  \tdplotsetmaincoords{70}{110}
  \begin{tikzpicture}[line cap=round, line join=round, >=Triangle]
  \clip(-2.19,-2.49) rectangle (2.66,2.58);
  \draw [shift={(0,0)}, lightgray, fill, fill opacity=0.1] (0,0) -- (56.7:0.4) arc (56.7:90.:0.4) -- cycle;
  \draw [shift={(0,0)}, lightgray, fill, fill opacity=0.1] (0,0) -- (-135.7:0.4) arc (-135.7:-33.2:0.4) -- cycle;
  \draw(0,0) circle (2cm);
  \draw [rotate around={0.:(0.,0.)},dash pattern=on 3pt off 3pt] (0,0) ellipse (2cm and 0.9cm);
  \draw (0,0)-- (0.70,1.07);
  \draw [->] (0,0) -- (0,2);
  \draw [->] (0,0) -- (-0.81,-0.79);
  \draw [->] (0,0) -- (2,0);
  \draw [dotted] (0.7,1)-- (0.7,-0.46);
  \draw [dotted] (0,0)-- (0.7,-0.46);
  \draw (-0.08,-0.3) node[anchor=north west] {$\varphi$};
  \draw (0.01,0.9) node[anchor=north west] {$\theta$};
  \draw (-1.01,-0.72) node[anchor=north west] {$\mathbf {\hat{x}}$};
  \draw (2.07,0.3) node[anchor=north west] {$\mathbf {\hat{y}}$};
  \draw (-0.5,2.6) node[anchor=north west] {$\mathbf {\hat{z}=|0\rangle}$};
  \draw (-0.4,-2) node[anchor=north west] {$-\mathbf {\hat{z}=|1\rangle}$};
  \draw (0.4,1.65) node[anchor=north west] {$|\psi\rangle$};
  \scriptsize
  \draw [fill] (0,0) circle (1.5pt);
  \draw [fill] (0.7,1.1) circle (0.5pt);
\end{tikzpicture}

  \small Bloch sphere representation of a qubit.
  \end{center}

  \item For each quantum gate $X,Y,Z,H,P(\hat{\theta})$ ($\hat{\theta}\in[0,2\pi)$ - this is sometimes referred to as the phase gate), describe qualitatively how each transforms $(\alpha,\beta)$, $(\theta,\phi)$, and their impact on measurement of the basis states after their application relative to the measurements of the original quantum state.
  \item Apply $H$ to $\ket{0}$, write the resulting state.
  \item Apply $H$ again, describe which basis state undergoes constructive/destructive interference and explain the outcome.
  \item Is the final state a superposition or a determined basis state? Justify.
\end{enumerate}
~~~

**Readable problem statement and learning interpretation:**

> (a) Any single-qubit state can be written as
> \[
> \ket{\psi}=\cos\!\left(\tfrac{\theta}{2}\right)\ket{0}+e^{i\phi}\sin\!\left(\tfrac{\theta}{2}\right)\ket{1},
> \]
> where \(\theta\in[0,\pi]\), \(\phi\in[0,2\pi)\). Derive \(\theta\) and \(\phi\) in terms of amplitudes \(\alpha,\beta\) for \(\ket{\psi}=\alpha\ket{0}+\beta\ket{1}\). State \((\theta,\phi)\) for \(\ket{0}\) and \(\ket{1}\).
>
> (b) For each quantum gate \(X,Y,Z,H,P(\hat{\theta})\) (\(\hat{\theta}\in[0,2\pi)\) — this is sometimes referred to as the phase gate), describe qualitatively how each transforms \((\alpha,\beta)\), \((\theta,\phi)\), and their impact on measurement of the basis states after their application relative to the measurements of the original quantum state.
>
> (c) Apply \(H\) to \(\ket{0}\), write the resulting state.
>
> (d) Apply \(H\) again, describe which basis state undergoes constructive/destructive interference and explain the outcome.
>
> (e) Is the final state a superposition or a determined basis state? Justify.

The original (a) also includes a Bloch-sphere diagram in the pinned source. Plain language: separate population balance from relative phase, track five gates both algebraically and geometrically, then explain why two Hadamards restore a definite basis state.

### B. What this tests; given and find

The problem tests polar representation of a normalized complex vector modulo global phase, Pauli/Hadamard/phase matrices, basis-probability effects, and amplitude interference. It appears after CNOT because the same state-vector discipline now acquires a geometric view and phase becomes operational.

**Given:** \(\alpha,\beta\in\mathbb C\) with \(|\alpha|^2+|\beta|^2=1\); computational-basis measurement; gates \(X,Y,Z,H,P(\hat\theta)\). **Find:** Bloch angles including poles, each gate's amplitude/angle/probability action, \(H|0\rangle\), \(H^2|0\rangle\), and physical interpretation.

### C. Prerequisites (QML0 §§3.3, 3.6 and §5)

| Concept | Definition and mathematical form | Physical meaning and why here |
|---|---|---|
| Global phase | \(e^{i\gamma}|\psi\rangle\) represents the same pure-state ray; \(|e^{i\gamma}c|^2=|c|^2\). | Remove one unobservable overall phase before assigning Bloch angles. |
| Relative phase | \(\phi=\arg\beta-\arg\alpha\pmod{2\pi}\), away from zero amplitudes. | Can change interference even when direct Z probabilities do not. |
| Bloch coordinates | \(\mathbf r=(\sin\theta\cos\phi,\sin\theta\sin\phi,\cos\theta)\). | \(\theta\) determines populations; \(\phi\) determines transverse direction. |
| Unitary gate | A matrix preserving norm, e.g. \(H=\frac1{\sqrt2}\begin{pmatrix}1&1\\1&-1\end{pmatrix}\). | Mixes or phases amplitudes before the Born rule is applied. |

### D. Derivation and full solution

**(a) Remove the global phase.** Write \(\alpha=|\alpha|e^{i\gamma}\), \(\beta=|\beta|e^{i\delta}\) when nonzero. Multiplying the whole ket by \(e^{-i\gamma}\) yields the canonical representative
\[
|\alpha||0\rangle+e^{i(\delta-\gamma)}|\beta||1\rangle.
\]
Because \(|\alpha|^2+|\beta|^2=1\) and \(\theta\in[0,\pi]\), identify \(\cos(\theta/2)=|\alpha|\), \(\sin(\theta/2)=|\beta|\). Hence
\[
\boxed{\theta=2\operatorname{atan2}(|\beta|,|\alpha|)
=2\arccos|\alpha|,\qquad
\phi=(\arg\beta-\arg\alpha)\bmod 2\pi}
\]
when both amplitudes are nonzero. The equivalent formula \(2\arcsin|\beta|\) also works. For \(|0\rangle\), \(\theta=0\); for \(|1\rangle\), \(\theta=\pi\). **At either pole, \(\phi\) is arbitrary/undefined as a physical coordinate** because the coefficient carrying that phase is zero or the remaining phase is global. Choosing \(\phi=0\) is a convention, not a uniquely inferred value.

**(b) Gate action.** Put \(r_x=\sin\theta\cos\phi,\ r_y=\sin\theta\sin\phi,\ r_z=\cos\theta\). The gate matrices and resulting amplitudes are
\[
\begin{array}{c|c|c}
G&G\text{ matrix}&G(\alpha,\beta)^T\\ \hline
X&\begin{pmatrix}0&1\\1&0\end{pmatrix}&(\beta,\alpha)^T\\
Y&\begin{pmatrix}0&-i\\i&0\end{pmatrix}&(-i\beta,i\alpha)^T\\
Z&\begin{pmatrix}1&0\\0&-1\end{pmatrix}&(\alpha,-\beta)^T\\
H&\frac1{\sqrt2}\begin{pmatrix}1&1\\1&-1\end{pmatrix}&((\alpha+\beta)/\sqrt2,(\alpha-\beta)/\sqrt2)^T\\
P(\hat\theta)&\begin{pmatrix}1&0\\0&e^{i\hat\theta}\end{pmatrix}&(\alpha,e^{i\hat\theta}\beta)^T.
\end{array}
\]
Their Bloch and measurement effects follow from these columns:

| Gate | Bloch-vector / angle action, modulo \(2\pi\) and pole ambiguity | Z-basis probabilities after gate |
|---|---|---|
| \(X\) | \((r_x,r_y,r_z)\mapsto(r_x,-r_y,-r_z)\); \((\theta,\phi)\mapsto(\pi-\theta,-\phi)\). | Swap: \(P'_0=|\beta|^2,\ P'_1=|\alpha|^2\). |
| \(Y\) | \(\mathbf r\mapsto(-r_x,r_y,-r_z)\); \((\theta,\phi)\mapsto(\pi-\theta,\pi-\phi)\). | Swap, as for X; factors \(\pm i\) are phases. |
| \(Z\) | \(\mathbf r\mapsto(-r_x,-r_y,r_z)\); \((\theta,\phi)\mapsto(\theta,\phi+\pi)\). | Unchanged: \((|\alpha|^2,|\beta|^2)\). |
| \(P(\hat\theta)\) | \(\mathbf r\) rotates about \(z\) by \(\hat\theta\); \((\theta,\phi)\mapsto(\theta,\phi+\hat\theta)\). | Unchanged directly; a later mixing gate can reveal the phase. |
| \(H\) | \(\mathbf r\mapsto(r_z,-r_y,r_x)\). Thus \(\theta'=\arccos(\sin\theta\cos\phi)\), \(\phi'=\operatorname{atan2}(-\sin\theta\sin\phi,\cos\theta)\) when off a pole. | \(P'_0=\frac12|\alpha+\beta|^2=\frac12+\operatorname{Re}(\alpha^*\beta)\), \(P'_1=\frac12|\alpha-\beta|^2=\frac12-\operatorname{Re}(\alpha^*\beta)\). |

The H probability expressions use \(|\alpha|^2+|\beta|^2=1\). In Bloch form they are \((1\pm r_x)/2\), rather than the original \((1\pm r_z)/2\). Therefore H can turn relative phase into a Z-basis population difference. These angle formulas describe the same physical ray; global factors introduced by X or Y do not change the Bloch point. At a new pole, the \(\operatorname{atan2}\) azimuth is physically arbitrary.

For basis-state spot checks: \(X|0\rangle=|1\rangle,\ Y|0\rangle=i|1\rangle,\ Z|1\rangle=-|1\rangle,\ H|0\rangle=|+\rangle,\ P(\hat\theta)|1\rangle=e^{i\hat\theta}|1\rangle\). The factors \(i,-1,e^{i\hat\theta}\) in these one-component states are global, so their direct measurement outcomes are unchanged from the corresponding basis ket.

**(c) First Hadamard.**
\[
H|0\rangle=\frac{|0\rangle+|1\rangle}{\sqrt2}=|+\rangle.
\]
The state is an equal computational-basis superposition; each Z outcome has probability \(1/2\).

**(d) Second Hadamard and interference.** Use \(H|0\rangle=(|0\rangle+|1\rangle)/\sqrt2\) and \(H|1\rangle=(|0\rangle-|1\rangle)/\sqrt2\):
\[
H|+\rangle
=\frac1{\sqrt2}\!\left(\frac{|0\rangle+|1\rangle}{\sqrt2}
+\frac{|0\rangle-|1\rangle}{\sqrt2}\right)
=\frac{2|0\rangle+0|1\rangle}{2}=|0\rangle.
\]
The two paths to \(|0\rangle\) add constructively; the two to \(|1\rangle\) cancel destructively. Amplitudes combine **before** squaring, so this is not a pair of independent random bit flips.

**(e) Final state:** the determined computational-basis state \(|0\rangle\), not a nontrivial superposition. Its Z probabilities are \((1,0)\).

### E. Why it works, physical meaning, and independent verification

An overall phase multiplies both amplitudes and cancels from all Born probabilities. Relative phase survives because a later matrix such as H sums amplitudes. Direct Z measurement sees only \(r_z\), whereas H before Z measurement makes the result depend on the original \(r_x\). Independently, \(H^2=\frac12\begin{pmatrix}1&1\\1&-1\end{pmatrix}^2=I_2\), confirming (d–e) for **every** input. For H, \(P'_0+P'_1=1\) because the \(\pm\operatorname{Re}(\alpha^*\beta)\) terms cancel. X/Y swap probabilities; Z/P leave them unchanged, consistent with the table. No simulator is required for this written problem.

### F. Expert checkpoints

| Potential weakness | Why it matters | Correct concept | How our work addresses it |
|---|---|---|---|
| Claiming arbitrary complex \(\alpha\) already equals nonnegative \(\cos(\theta/2)\) | Ignores global phase. | Fix a ray representative first. | Explicitly removes \(e^{i\gamma}\). |
| Assigning a unique \(\phi\) to \(|0\rangle\) or \(|1\rangle\) | Azimuth is undefined at poles. | Phase of a zero coefficient is meaningless. | States pole ambiguity. |
| Saying Z/P cannot matter because direct counts stay fixed | Relative phase can be read out later. | Interference after a mixing gate. | Derives H's \(\operatorname{Re}(\alpha^*\beta)\) term. |
| Treating Y's \(i\) as a changed basis probability | Confuses global/relative phase with magnitude. | Born rule uses modulus. | Gives both amplitude and probability actions. |
| Explaining \(H^2|0\rangle\) as two randomizations | Loses coherence. | Add amplitudes before squaring. | Shows constructive and destructive terms. |

**Alternative check:** the Bloch map \(H:(r_x,r_y,r_z)\mapsto(r_z,-r_y,r_x)\) takes \(|0\rangle\)'s north pole to \(+x\), then back to the north pole; the matrix product \(H^2=I\) agrees.

### G. What to remember and later relevance

**Core lesson:** \(\theta\) encodes population balance, \(\phi\) relative phase, and H converts an appropriate phase-sensitive component into a measurable Z population. **Equations:** \(\theta=2\operatorname{atan2}(|\beta|,|\alpha|)\), \(\phi=\arg\beta-\arg\alpha\), \(P_H(0)=(1+2\operatorname{Re}\alpha^*\beta)/2\), \(H^2=I\). **Intuition:** coherent branches can cancel or reinforce; phase-only gates may be invisible to immediate Z measurement. **Later-course dependency:** Problem 4's superposition circuits and QML2's fidelity versus histogram distinction.

**What the homework establishes:** ideal single-qubit phase, gate, and interference relationships. **What may later be investigated:** phase-sensitive observables, dephasing and control error in a physical device (QML1), or feature maps/measurement choices in QML. These hand calculations do not validate a research architecture.

### H. Active recall

**Questions:** (1) Why may \(\alpha\) be made nonnegative in the Bloch form? (2) What happens to \(\phi\) at a pole? (3) Which of X/Y/Z/P change immediate Z probabilities? (4) What original-state quantity does H reveal in Z counts? (5) Why does \(H^2|0\rangle=|0\rangle\)?

**Answers:** (1) Remove a common global phase. (2) It is physically arbitrary. (3) X and Y swap them; Z and P preserve them. (4) \(r_x=2\operatorname{Re}(\alpha^*\beta)\). (5) The \(|1\rangle\) path amplitudes cancel while the \(|0\rangle\) paths add; equivalently \(H^2=I\).

## Problem 4 — From Tensor Products to Circuits in Qiskit (25 points)

![Exact outcome distributions: part (d) applies H to q0 only; part (e) applies H to all three qubits.](./figures/problem4_circuit_outcomes.png)

### A. Exact instructor problem and plain-language task

**Verbatim pinned instructor LaTeX for this numbered problem** (including its summary, figures where present, and every subpart):

~~~tex
\problem{From Tensor Products to Circuits in Qiskit}{25}
\begin{summary}
This problem connects the mathematical definition of multi-qubit operations using tensor products to their implementation in Qiskit. You will practice reasoning about superposition states mathematically and then reproduce them in circuit form.
\end{summary}

\begin{enumerate}[label=(\alph*)]
  \item Prove that $(H\otimes H)\ket{00} = (H\ket{0})\otimes(H\ket{0})$. Explain why this generalizes to $n$ qubits.
  \item Explain how tensoring unitaries allows us to define operations on multi-qubit systems.
  \item Construct a Qiskit circuit on two qubits applying $H$ to both, and verify it matches your result in (a).
  \item On three qubits: Case 1—apply $H$ to $q_0$ only, then CNOT(0$\to$1) \newline (with convention being $\text{control qubit number} \to \text{ target qubit number)}$ starting qubit indexing at 0 because we count our qubits like real computer scientists. Case 2—apply $H$ to $q_0$ only, then CNOT(1$\to$0).
  In both cases, show mathematically (tensor product or simulation) how you can do an analogous computation to what was done in (a) for more general multi qubit systems. Hint: If nothing is done to a qubit at a "step" of the quantum circuit, use the identity matrix as the quantum operation on it ("the do nothing gate"). See the circuits below to get an idea of each case - following Case 1 and then Case 2 (the figures show $H$ on every qubit; you should apply $H$ only to $q_0$).
  \item \textit{Food for thought:} if you instead apply $H$ to \emph{all} three qubits before the CNOT (as in the figures), show that Case 1 and Case 2 produce exactly the same state. Why does the CNOT direction not matter here? (Hint: what is CNOT$\ket{++}$? Is $\ket{+++}$ entangled?)
  \includegraphics[]{qc_case1.pdf}
  \includegraphics[]{qc_case2.pdf}
\end{enumerate}
~~~

**Readable problem statement and learning interpretation:**

> (a) Prove that \((H\otimes H)\ket{00}=(H\ket{0})\otimes(H\ket{0})\). Explain why this generalizes to \(n\) qubits.
>
> (b) Explain how tensoring unitaries allows us to define operations on multi-qubit systems.
>
> (c) Construct a Qiskit circuit on two qubits applying \(H\) to both, and verify it matches your result in (a).
>
> (d) On three qubits: Case 1—apply \(H\) to \(q_0\) only, then CNOT(0\(\to\)1) (control qubit number \(\to\) target qubit number, starting qubit indexing at 0). Case 2—apply \(H\) to \(q_0\) only, then CNOT(1\(\to\)0). In both cases, show mathematically (tensor product or simulation) how you can do an analogous computation to what was done in (a) for more general multi qubit systems. *Hint:* If nothing is done to a qubit at a “step” of the quantum circuit, use the identity matrix as the quantum operation on it (“the do nothing gate”). The source figures show H on every qubit; apply H only to \(q_0\) for this part.
>
> (e) *Food for thought:* if you instead apply \(H\) to all three qubits before the CNOT (as in the figures), show that Case 1 and Case 2 produce exactly the same state. Why does the CNOT direction not matter here? (Hint: what is CNOT\(\ket{++}\)? Is \(\ket{+++}\) entangled?)

The source includes two circuit figures in the pinned archive. Plain language: prove the product-operation rule, implement it, then distinguish the effect of reversing CNOT control when only one input wire is superposed versus when every wire is in \(|+\rangle\).

### B. What this tests; given and find

This problem bridges abstract tensor operators and indexed circuit wires. It tests distributivity/linearity, operator composition, identity on untouched wires, controlled-gate direction, product versus entangled states, and simulator readout conventions.

**Given:** all-zero inputs, \(H|0\rangle=|+\rangle\), three named qubits \(q_0,q_1,q_2\), CNOT directions in (d–e). **Find:** proof and generalization, circuit outputs, state evolution for both three-qubit cases, equality for all-H cases, and measured verification.

### C. Prerequisites (QML0 §§3.4–3.5 and circuit/Qiskit sections)

| Concept | Definition and mathematical form | Physical meaning and why here |
|---|---|---|
| Product-operator rule | \((A\otimes B)(|u\rangle\otimes|v\rangle)=A|u\rangle\otimes B|v\rangle\). | Independent gates act on their own wires. |
| Identity on untouched wires | \(I|0\rangle=|0\rangle,\ I|1\rangle=|1\rangle\). | A wire omitted from a circuit step retains its state. |
| Circuit composition | \(U_2U_1|\psi\rangle\) applies \(U_1\) first. | Prevents gate-order reversal. |
| Product versus entangled | Product state factors into single-wire kets; Bell-like \((|00\rangle+|11\rangle)/\sqrt2\) does not. | Distinguishes Case 1 from all-H. |
| Counts | 1024 ideal simulator samples approximate theoretical probabilities. | Confirms supported outcomes but is not itself a phase-complete state proof. |

### D. Derivation and full solution

**(a) Product operation.** Since \(|00\rangle=|0\rangle\otimes|0\rangle\), the tensor definition gives
\[
(H\otimes H)|00\rangle=(H|0\rangle)\otimes(H|0\rangle)
=|+\rangle\otimes|+\rangle
=\tfrac12(|00\rangle+|01\rangle+|10\rangle+|11\rangle).
\]
The distributive expansion is valid because tensor product is bilinear. For \(n\) factors, repeated associativity and the same product rule give
\[
\left(\bigotimes_{j=0}^{n-1}U_j\right)\left(\bigotimes_{j=0}^{n-1}|\psi_j\rangle\right)
=\bigotimes_{j=0}^{n-1}U_j|\psi_j\rangle.
\]
In particular, \(H^{\otimes n}|0\rangle^{\otimes n}=2^{-n/2}\sum_{x\in\{0,1\}^n}|x\rangle\). This rule applies directly to product inputs and local operators; an entangling CNOT is a joint operator, not generally a product of one-qubit gates.

**(b) Unitaries on a joint space.** \(U_j\) acting on a two-dimensional factor makes \(\bigotimes_jU_j\) a \(2^n\times2^n\) operator. It is unitary because
\[
(\bigotimes_jU_j)^\dagger(\bigotimes_jU_j)
=\bigotimes_j(U_j^\dagger U_j)=\bigotimes_j I=I_{2^n}.
\]
For example, \(H\otimes I\otimes I\) applies H to written leftmost \(q_0\) and leaves \(q_1,q_2\) untouched. A controlled two-qubit gate embedded on selected wires is also a unitary on the full joint space, but its correlated action must be evaluated on each relevant branch.

**(c) Two-wire circuit.** Apply H to both \(q_0\) and \(q_1\) from \(|00\rangle\). The predicted state is the four-term state in (a), so each Z-basis outcome has probability \(1/4\). The notebook's statevector has amplitude \(0.5\) for each course-order ket. With 1024 Aer shots and seed 739, Qiskit count strings \(q_1q_0\) were \(00:257,\ 01:255,\ 10:266,\ 11:246\). Their sum is 1024 and finite-shot deviations from 256 are expected.

**(d) Three-wire circuits; written ket order \(q_0q_1q_2\).** After \(H\otimes I\otimes I\),
\[
|\psi_1\rangle=\tfrac1{\sqrt2}(|000\rangle+|100\rangle).
\]
Case 1 applies CNOT(0→1). It fixes \(|000\rangle\) but sends \(|100\rangle\to|110\rangle\), so
\[
\boxed{|\psi_{\rm case\,1}\rangle=(|000\rangle+|110\rangle)/\sqrt2.}
\]
The \(q_0q_1\) pair is Bell-like and cannot factor; \(q_2\) remains \(|0\rangle\). Case 2 applies CNOT(1→0). Since \(q_1=0\) on **both** branches, neither target flips:
\[
\boxed{|\psi_{\rm case\,2}\rangle=(|000\rangle+|100\rangle)/\sqrt2=|+\rangle_0|0\rangle_1|0\rangle_2.}
\]
The notebook statevectors agree exactly. Qiskit printed strings \(q_2q_1q_0\): Case 1 \(000:521,\ 011:503\); Case 2 \(000:521,\ 001:503\). The course-order \(|110\rangle\) appears as Qiskit \(011\), and \(|100\rangle\) as \(001\). Both supported outcomes have theoretical probability \(1/2\).

**(e) H on all wires first.** The intermediate state is \(|+\rangle_0|+\rangle_1|+\rangle_2\). For either CNOT direction, the target is \(|+\rangle\) and \(X|+\rangle=|+\rangle\). More explicitly, a control-zero branch leaves \(|+\rangle\) unchanged and a control-one branch applies X, also leaving it unchanged. Therefore
\[
\mathrm{CNOT}_{0\to1}|+++\rangle
=\mathrm{CNOT}_{1\to0}|+++\rangle
=|+++\rangle
=2^{-3/2}\sum_{x\in\{0,1\}^3}|x\rangle.
\]
This is a **product state**, not entangled, despite eight nonzero basis amplitudes. The equality is special to this input and does not make the two CNOT operators equal. Aer statevectors were equivalent; each direction yielded, in \(q_2q_1q_0\) order, \(000:139,\ 001:124,\ 010:127,\ 011:134,\ 100:131,\ 101:127,\ 110:124,\ 111:118\), versus ideal \(128\) each.

### E. Runnable Qiskit implementation and theory-to-code map

The full executed notebook is linked above. This stand-alone code reproduces the Problem 4 circuits and count checks in an environment with Qiskit and Qiskit Aer:
~~~python
from qiskit import QuantumCircuit, transpile
from qiskit.quantum_info import Statevector
from qiskit_aer import AerSimulator

sim = AerSimulator(seed_simulator=739)
def counts(qc):
    measured = QuantumCircuit(qc.num_qubits, qc.num_qubits)
    measured.compose(qc, inplace=True)
    measured.measure(range(qc.num_qubits), range(qc.num_qubits))
    return sim.run(transpile(measured, sim, seed_transpiler=739),
                   shots=1024).result().get_counts()

both = QuantumCircuit(2)
both.h([0, 1])
case1 = QuantumCircuit(3)
case1.h(0); case1.cx(0, 1)
case2 = QuantumCircuit(3)
case2.h(0); case2.cx(1, 0)
all1 = QuantumCircuit(3)
all1.h([0, 1, 2]); all1.cx(0, 1)
all2 = QuantumCircuit(3)
all2.h([0, 1, 2]); all2.cx(1, 0)
for label, qc in [("both H", both), ("case 1", case1),
                  ("case 2", case2), ("all H 0->1", all1),
                  ("all H 1->0", all2)]:
    print(label, Statevector.from_instruction(qc).data, counts(qc))
assert Statevector.from_instruction(all1).equiv(Statevector.from_instruction(all2))
~~~

The H calls implement tensor-product local H operations; omitted wires receive identity. The \(\mathrm{cx}(control,target)\) argument order matches the prompt. Statevector entries use Qiskit's little-endian array indexing, while the algebra above uses written course-order kets. Measuring \(q_j\) into classical bit \(c_j\) makes displayed strings \(c_{n-1}\cdots c_0\). Counts provide sampled Z distributions; the statevector check verifies phases and the exact all-H equality.

### F. Independent verification, physical meaning, and expert checkpoints

The analytic ket expansion and Qiskit statevector agree branch by branch. Each state is normalized: two terms of magnitude \(1/\sqrt2\) in (d), or eight of magnitude \(1/\sqrt8\) in (e). The measured count totals are 1024 in every run. The alternative invariant \(X|+\rangle=|+\rangle\) explains (e) without enumerating eight basis mappings.

| Potential weakness | Why it matters | Correct concept | How our work addresses it |
|---|---|---|---|
| Copying the source figures' all-H gates into (d) | Would solve a different circuit. | Read text's H-only-on-\(q_0\) instruction. | Separates (d) from (e). |
| Ignoring identity on \(q_2\) | Makes three-wire evolution ambiguous. | \(H\otimes I\otimes I\). | States operator and unchanged third wire. |
| Treating CNOT directions as generally equal | They differ on Case 1's input. | Control is a named qubit. | Derives distinct Case 1/2 outputs. |
| Calling \(|+++\rangle\) entangled | Multiple branches are insufficient. | Product-factorization test. | Writes \(|+\rangle^{\otimes3}\). |
| Reading Qiskit \(011\) as course ket \(|011\rangle\) | Reverses qubit labels. | Classical strings print high bit first. | Maps \(011\leftrightarrow|110\rangle\). |
| Using counts alone to prove state equality | Relative phase could be hidden. | Statevector/equivalent-basis check. | Checks exact statevectors as well. |

### G. What to remember and later relevance

**Core lesson:** local tensor unitaries act factorwise; controlled gates can entangle depending on input; Qiskit strings require explicit mapping. **Equations:** product-operator identity, \(H^{\otimes n}|0^n\rangle=2^{-n/2}\sum_x|x\rangle\), \(X|+\rangle=|+\rangle\). **Intuition:** a gate's effect depends on both its wire direction and the target/control state. **Later-course dependency:** Problem 5's indexed controls and measurements; QML2's circuit search and phase-sensitive fidelity.

**What the homework establishes:** ideal circuit states and ideal simulator agreement for specified inputs. **What may later be investigated:** hardware mapping, gate noise, or whether a QML circuit metric detects relative phase. No physical device or external research system is evaluated here.

### H. Active recall

**Questions:** (1) Why does \(H^{\otimes n}|0^n\rangle\) have \(2^n\) equal amplitudes? (2) What are the two states in (d)? (3) Why do the two CNOT directions agree in (e)? (4) Is \(|+++\rangle\) entangled? (5) What does Qiskit string 011 mean for \(q_0q_1q_2\)?

**Answers:** (1) Repeated factorwise H and bilinear expansion. (2) \((|000\rangle+|110\rangle)/\sqrt2\) and \((|000\rangle+|100\rangle)/\sqrt2\). (3) \(X|+\rangle=|+\rangle\). (4) No; it factors into three \(|+\rangle\) states. (5) \(q_2q_1q_0=011\), hence course-order \(|110\rangle\).

## Problem 5 — Half and Full Quantum Adder: Implementation and Interpretation (30 points)

![Full-adder outputs for every A, B, Cin input; the Cin=0 rows also check the half-adder outputs.](./figures/problem5_full_adder_truth_table.png)

### A. Exact instructor problem and plain-language task

**Verbatim pinned instructor LaTeX for this numbered problem** (including its summary, figures where present, and every subpart):

~~~tex
\problem{Half and Full Quantum Adder: Implementation and Interpretation}{30}
\begin{summary}
In this problem you will connect provided circuit diagrams for a 1-bit half adder and full adder (with carry) to its behavior (see Figures~\ref{fig:halfadder} and~\ref{fig:fulladder}). You will implement the circuits (which are made of CNOT and Toffoli gates), reason about one input by hand, and then validate all input cases on a simulator. Measure S the sum and C the carry for given inputs. A half adder is an adder that only calculates the sum and the carry for a stand alone add - not additions that can be strung together. However, a full adder can do chain addition to do "ripple-carry adders".

\textit{The Toffoli (CCX) gate was not covered in lecture:} it is a three-qubit gate with two controls and one target that flips the target if and only if both controls are $\ket{1}$, i.e. $\ket{a,b,c}\mapsto\ket{a,b,c\oplus ab}$. In the computational basis its $8\times 8$ matrix is the identity except that the last two basis states $\ket{110}$ and $\ket{111}$ are swapped. In Qiskit it is \texttt{qc.ccx(control1, control2, target)}.
\end{summary}
\begin{figure}[h!]
  \centering
  \includegraphics[width=\textwidth]{halfadder.png}
  \caption{Half Quantum Adder (without ripple(chain)-carry). Wires top to bottom are $q_0=A$, $q_1=B$, $q_2=\ket{0}$; outputs $S$ on $q_1$ and $C$ on $q_2$.}
  \label{fig:halfadder}
\end{figure}

\begin{figure}[h!]
  \centering
  \includegraphics[width=\textwidth]{fulladder.png}
  \caption{Full Quantum Adder (with ripple(chain)-carry). Wires top to bottom are $q_0=A$, $q_1=B$, $q_2=C_{in}$, $q_3=\ket{0}$; outputs $S$ on $q_2$ and $C_{out}$ on $q_3$.}
  \label{fig:fulladder}
\end{figure}

\begin{enumerate}[label=(\alph*)]

  \item Work out by hand what happens to $\ket{110}$ as input to the half quantum adder and $\ket{1100}$ for the full adder. What is the final expected quantum state before measurement?
  \item Implement both circuits in Qiskit, initializing carry to $\ket{0}$ and setting inputs with $X$ gates as needed.
  \item Run for inputs $(q_0,q_1)\in\{00,01,10,11\}$ for the half adder. Do the same with the full adder, with $C_{in}=q_2=0$. Use conditional $X$ gates to prepare inputs that start in the ground state on the appropriate qubit. Record outputs $(q_1,q_2)$ which represent the value of the addition and if carry is present, respectively for the half adder, and measure $(q_2,q_3)$ for the full adder, which hold $S$ and $C_{out}$ respectively.
  \item Compare the quantum adder results using a simulator did you find what you expected? You are in no way required to, but feel free to run this same circuit on Qiskits real quantum computers instead of simulator - did your results change?
\end{enumerate}

\textbf{Important note:} You may optionally run your ripple-carry adder on IBM’s real quantum hardware (e.g., 100 shots) to compare expectation vs. reality. Running on real hardware requires an IBM Quantum account (the free Open Plan is sufficient; no credit card is needed) and is \emph{not required}. You will not be penalized for not doing this.
If you do try it, you will see that while the simulator yields perfect results, the hardware produces noisy results with a distribution of outcomes. This illustrates why NISQ-era devices must eventually give way to fault-tolerant error-corrected quantum computers (FTECQC) with logical qubits to achieve reliable results.
~~~

**Readable problem statement and learning interpretation:**

> In this problem you will connect provided circuit diagrams for a 1-bit half adder and full adder (with carry) to its behavior. Implement the circuits (which are made of CNOT and Toffoli gates), reason about one input by hand, and then validate all input cases on a simulator. Measure S the sum and C the carry for given inputs. A half adder calculates the sum and carry for a stand-alone addition; a full adder can be chained for ripple-carry addition.
>
> The Toffoli (CCX) gate is a three-qubit gate with two controls and one target that flips the target iff both controls are \(\ket1\): \(\ket{a,b,c}\mapsto\ket{a,b,c\oplus ab}\). Its computational-basis \(8\times8\) matrix is the identity except that \(\ket{110}\) and \(\ket{111}\) swap; Qiskit uses qc.ccx(control1, control2, target).
>
> Half-adder figure caption: wires top to bottom are \(q_0=A,\ q_1=B,\ q_2=\ket0\); outputs \(S\) on \(q_1\) and \(C\) on \(q_2\). Full-adder figure caption: wires top to bottom are \(q_0=A,\ q_1=B,\ q_2=C_{in},\ q_3=\ket0\); outputs \(S\) on \(q_2\) and \(C_{out}\) on \(q_3\).
>
> (a) Work out by hand what happens to \(\ket{110}\) as input to the half quantum adder and \(\ket{1100}\) for the full adder. What is the final expected quantum state before measurement?
>
> (b) Implement both circuits in Qiskit, initializing carry to \(\ket0\) and setting inputs with X gates as needed.
>
> (c) Run for inputs \((q_0,q_1)\in\{00,01,10,11\}\) for the half adder. Do the same with the full adder, with \(C_{in}=q_2=0\). Use conditional X gates to prepare inputs from the ground state. Record outputs \((q_1,q_2)\) for half adder and \((q_2,q_3)\) for full adder, holding \(S,C\).
>
> (d) Compare the quantum adder results using a simulator: did you find what you expected? Running on real quantum hardware is optional, not required.

The exact diagrams are in the pinned source ZIP; their gate order is transcribed and checked below. The source's summary calls this a “1-bit ripple-carry adder,” while the detailed task assigns one half adder and one full-adder stage. A chain of multiple stages is **Bonus B**, not a required Problem 5 implementation.

### B. What this tests; given and find

The problem tests translating a circuit diagram into indexed reversible gates, interpreting XOR/AND arithmetic, distinguishing sum from carry, preparing basis inputs, and mapping measured bits. It follows Problem 4 because the same basis-mapping and wire-order discipline now implements classical arithmetic reversibly.

**Given:** all registers initialize at \(|0\rangle\); A and B prepared by X as needed; half carry ancilla \(q_2=0\); full \(C_{in}=q_2\), output ancilla \(q_3=0\); CCX and CX truth rules; diagram gate order. **Find:** two hand-traced output kets, runnable circuits, all four requested input cases for both, theory/count comparison. Full \(C_{in}=1\) cases are extra independent verification.

### C. Prerequisites (QML0 controlled-gate/circuit sections; prompt's CCX definition)

| Concept | Definition and mathematical form | Physical meaning and why here |
|---|---|---|
| Basis encoding | \(X|0\rangle=|1\rangle\); apply X to a wire iff its input bit is 1. | Prepares classical bit values as computational-basis kets. |
| CNOT | \((a,b)\mapsto(a,b\oplus a)\). | Computes XOR into a target without changing the control. |
| Toffoli / CCX | \((a,b,c)\mapsto(a,b,c\oplus ab)\). | Computes the AND condition into a target; reversible as a full mapping. |
| Half-adder arithmetic | \(S=A\oplus B,\ C=AB\). | One binary digit's sum bit and carry. |
| Full-adder arithmetic | \(S=A\oplus B\oplus C_{in}\), \(C_{out}=AB\lor[(A\oplus B)C_{in}]\). | A carry from the previous digit affects both outputs. |
| Measurement | \(q_j\to c_k\), with printed classical string high index first. | Prevents interpreting Qiskit “10” as \((S,C)=(1,0)\) when it is \(CS\). |

### D. Diagram-to-algebra derivation and hand traces

**Half adder diagram:** CCX(0,1,2), then CX(0,1). Starting \(|A,B,0\rangle\), CCX writes \(AB\) into \(q_2\), then CX writes \(A\oplus B\) into \(q_1\):
\[
\boxed{|A,B,0\rangle\ \longmapsto\ |A,A\oplus B,AB\rangle.}
\]
For the requested \(|110\rangle\), the sequential states are
\[
|110\rangle\xrightarrow{\mathrm{CCX}(0,1,2)}|111\rangle
\xrightarrow{\mathrm{CX}(0,1)}\boxed{|101\rangle}.
\]
Thus \(A=1,\ S=0,\ C=1\), correctly representing \(1+1=10_2\). The final ket is a definite basis state before measurement.

**Full adder diagram:** reading left to right: CCX(0,1,3), CX(0,1), CCX(1,2,3), CX(1,2), CX(0,1). Let \(t=A\oplus B\). The first CCX writes \(AB\) to \(q_3\); the first CX temporarily makes \(q_1=t\); the next CCX writes \(tC_{in}\) into \(q_3\), so \(q_3=AB\oplus tC_{in}\). The terms cannot both be 1: \(AB=1\) implies \(t=0\). Hence their XOR equals their OR and this is the full-adder carry. CX(1,2) makes \(q_2=C_{in}\oplus t=S\). The last CX restores \(q_1=B\), preserving both input registers:
\[
\boxed{|A,B,C_{in},0\rangle\ \longmapsto\
|A,B,A\oplus B\oplus C_{in},\ AB\lor((A\oplus B)C_{in})\rangle.}
\]
For the requested \(|1100\rangle\), the complete trace is
\[
\begin{aligned}
|1100\rangle
&\xrightarrow{\mathrm{CCX}(0,1,3)}|1101\rangle
\xrightarrow{\mathrm{CX}(0,1)}|1001\rangle\\
&\xrightarrow{\mathrm{CCX}(1,2,3)}|1001\rangle
\xrightarrow{\mathrm{CX}(1,2)}|1001\rangle
\xrightarrow{\mathrm{CX}(0,1)}\boxed{|1101\rangle}.
\end{aligned}
\]
Thus \(A=B=1,\ S=0,\ C_{out}=1\). The equality of the intermediate and final \(|1101\rangle\) is specific to this input; the temporary B toggle is still essential for general inputs.

### E. Required truth tables and measurement interpretation

The four required pairs, with half \(q_2=0\) and full \(C_{in}=q_2=0\), give:

| \(A,B\) | Half final \(|q_0q_1q_2\rangle\) | Full final \(|q_0q_1q_2q_3\rangle\) | \((S,C)\) | Printed \(c_1c_0=CS\), both circuits | Ideal counts, 1024 shots |
|---|---|---|---|---|---|
| 00 | \(|000\rangle\) | \(|0000\rangle\) | \((0,0)\) | 00 | 1024 of 00 |
| 01 | \(|010\rangle\) | \(|0110\rangle\) | \((1,0)\) | 01 | 1024 of 01 |
| 10 | \(|110\rangle\) | \(|1010\rangle\) | \((1,0)\) | 01 | 1024 of 01 |
| 11 | \(|101\rangle\) | \(|1101\rangle\) | \((0,1)\) | 10 | 1024 of 10 |

For half, measure \(q_1\to c_0=S,\ q_2\to c_1=C\). For full, measure \(q_2\to c_0=S,\ q_3\to c_1=C_{out}\). Qiskit displays \(c_1c_0\), so “10” means carry 1 and sum 0, not the reverse. The notebook executed these eight required circuits on ideal Aer and returned exactly the counts shown. Each basis input evolves to one basis output under these reversible gates, so there is no intrinsic sampling spread in an ideal noiseless simulator.

**Extra full-adder check with \(C_{in}=1\):**

| \(A,B,C_{in}\) | \((S,C_{out})\) | Qiskit \(CS\) | Aer 1024-shot count |
|---|---|---|---|
| 001 | (1,0) | 01 | 1024 of 01 |
| 011 | (0,1) | 10 | 1024 of 10 |
| 101 | (0,1) | 10 | 1024 of 10 |
| 111 | (1,1) | 11 | 1024 of 11 |

These extra cases verify the carry-in logic and the temporarily altered B wire, which the required \(C_{in}=0\) set alone would not exercise fully.

### F. Complete runnable Qiskit implementation and theory-to-code map

The [executed notebook](./Homework_1-Qiskit-Verification.ipynb) includes statevector hand-trace checks and saved counts. This stand-alone implementation reproduces the required cases:
~~~python
from qiskit import QuantumCircuit, transpile
from qiskit_aer import AerSimulator

SHOTS = 1024
sim = AerSimulator(seed_simulator=739)

def half(a, b):
    qc = QuantumCircuit(3, 2)
    if a: qc.x(0)
    if b: qc.x(1)
    qc.ccx(0, 1, 2)
    qc.cx(0, 1)
    qc.measure(1, 0)  # sum -> c0
    qc.measure(2, 1)  # carry -> c1
    return qc

def full(a, b, cin):
    qc = QuantumCircuit(4, 2)
    if a: qc.x(0)
    if b: qc.x(1)
    if cin: qc.x(2)
    qc.ccx(0, 1, 3)
    qc.cx(0, 1)
    qc.ccx(1, 2, 3)
    qc.cx(1, 2)
    qc.cx(0, 1)
    qc.measure(2, 0)  # sum -> c0
    qc.measure(3, 1)  # carry-out -> c1
    return qc

for a in (0, 1):
    for b in (0, 1):
        for name, qc in (("half", half(a, b)), ("full", full(a, b, 0))):
            compiled = transpile(qc, sim, seed_transpiler=739)
            result = sim.run(compiled, shots=SHOTS).result().get_counts()
            expected = f"{a & b}{a ^ b}"  # displayed c1c0 = carry,sum
            assert result == {expected: SHOTS}
            print(name, a, b, result)
~~~

The conditional X calls encode input 1s, not an in-circuit classical branch on measurement. The CCX/CX calls follow the diagram order exactly. The last full-adder CX restores B after it was used to compute \(t=A\oplus B\). Measurement occurs only after arithmetic; it returns classical S/C bits and ends coherence in those output wires. The notebook additionally verifies all four \(C_{in}=1\) cases.

### G. Independent verification, physical meaning, and expert checkpoints

An algebraic check uses the Boolean identity \(C_{out}=AB\lor AC_{in}\lor BC_{in}\), equivalent to \(AB\lor(A\oplus B)C_{in}\). The eight full-adder truth-table rows match this identity and the simulated outputs. Statevector checks independently returned \(|101\rangle\) for half input \(|110\rangle\) and \(|1101\rangle\) for full input \(|1100\rangle\). The gates are reversible on the **whole register**, preserving inputs/ancilla information; merely mapping two input bits to two output bits is not the entire unitary.

| Potential weakness | Why it matters | Correct concept | How our work addresses it |
|---|---|---|---|
| Reversing CCX and CX in the half diagram | Carry and sum wires could be wrong. | Read left-to-right gate sequence. | Hand-traces every gate. |
| Omitting full-adder final CX | B would remain \(A\oplus B\). | Restore the temporary work wire. | Shows \(q_1=t\) then \(q_1=B\). |
| Using \(AB\oplus tC_{in}\) as OR without justification | XOR and OR differ when terms overlap. | Here \(AB=1\Rightarrow t=0\). | Proves mutual exclusivity. |
| Calling \(q_2\) carry-out in the full circuit | \(q_2\) holds sum after computation. | Follow diagram's output labels. | Measures \(q_2=S,\ q_3=C_{out}\). |
| Reading “10” as sum 1, carry 0 | Qiskit prints classical bits in reverse index order. | \(c_1c_0=CS\). | Explicit mapping and table. |
| Assuming deterministic ideal counts imply hardware perfection | Physical gates/readout can be noisy. | Ideal simulator versus physical device. | Makes only ideal-simulator claims. |

### H. What to remember and later relevance

**Core lesson:** CCX computes a conditional AND into a target, CX computes XOR, and reversible wire bookkeeping matters as much as the final arithmetic. **Equations:** \(S=A\oplus B\oplus C_{in}\), \(C_{out}=AB\lor(A\oplus B)C_{in}\). **Intuition:** basis-state arithmetic is deterministic under ideal gates; a superposition input would evolve coherently by linearity, but this problem tests basis inputs. **Later-course dependency:** multi-bit arithmetic, reversible oracles, resource/depth analysis, and interpreting physical noise (QML1).

**What the homework establishes:** correct ideal one-bit half/full-adder logic and simulator verification for all requested cases. **What may later be investigated:** chaining stages, ancilla reuse/uncomputation, native-gate cost, noise propagation, or QML feature/oracle designs. The present counts are not evidence of speedup or hardware reliability.

### I. Active recall

**Questions:** (1) What does CCX(0,1,2) do on \(|110\rangle\)? (2) Why does the full adder temporarily change B? (3) Why is \(AB\oplus(A\oplus B)C_{in}\) a valid carry formula? (4) Which wires hold S and C in each circuit? (5) Why does Qiskit print 10 for \(1+1\)? (6) Why are ideal counts deterministic here?

**Answers:** (1) It changes the last bit to 1, giving \(|111\rangle\). (2) To compute \(A\oplus B\) as a control for the carry-in term, then restore B. (3) The two product terms cannot both be 1. (4) Half \(q_1,q_2\); full \(q_2,q_3\). (5) \(c_1c_0=CS=10\), meaning carry 1, sum 0. (6) Each computational-basis input is mapped by reversible classical gates to one basis output in the ideal model.

## Cross-Problem Knowledge Graph

\[
\text{single-qubit state}
\longrightarrow \text{orthonormal projection / Born rule}
\longrightarrow \text{normalization}
\longrightarrow \text{tensor-product basis}
\longrightarrow \text{controlled unitary / direction}
\longrightarrow \text{Bloch relative phase}
\longrightarrow \text{interference}
\longrightarrow \text{indexed Qiskit circuit and measurement}
\longrightarrow \text{reversible arithmetic}.
\]
Problem 1 fixes what an amplitude and probability mean. Problem 2 expands the basis and makes control direction operational. Problem 3 reveals information that direct computational-basis probabilities miss. Problem 4 turns the same algebra into circuits while exposing bit-order and entanglement distinctions. Problem 5 applies controlled gates to a reversible Boolean computation and checks its measured outputs.

## Final Homework Synthesis

### Major concepts learned

Normalized pure states, basis-dependent measurement, tensor products, unitarity, controlled gates, global versus relative phase, Bloch coordinates, coherent interference, product versus entangled states, ideal circuit simulation, and reversible half/full-adder logic.

### Important equations

\[
P(j)=|\langle j|\psi\rangle|^2,\quad
\sum_jP(j)=1,\quad
U^\dagger U=I,\quad
(A\otimes B)(|u\rangle\otimes|v\rangle)=A|u\rangle\otimes B|v\rangle,
\]
\[
H^{\otimes n}|0^n\rangle=2^{-n/2}\sum_x|x\rangle,\quad
S=A\oplus B\oplus C_{in},\quad
C_{out}=AB\lor(A\oplus B)C_{in}.
\]

### Mathematical techniques learned

Expand an orthonormal basis overlap; take complex modulus squared; track matrix columns by basis input; prove unitarity by an adjoint identity or orthonormal columns; remove global phase to obtain Bloch angles; evaluate a circuit branchwise; verify tensor identities and Boolean formulas independently of code.

### Quantum intuition gained

A state is not a pre-existing list of sampled outcomes. Gates transform amplitudes before measurement. Phase may be invisible to direct Z counts but become visible after H. CNOT can produce entanglement on one input and leave a product state invariant on another. A deterministic ideal adder count is a property of the chosen basis input and noiseless model, not a claim about physical hardware.

### Qiskit skills gained

Prepare basis inputs with X, address H/CX/CCX by numbered wire, preserve circuit order, obtain statevectors, measure selected output wires, map \(c_1c_0\) to \(CS\), run Aer with specified shots/seed, and compare counts with theoretical probabilities. The [notebook](./Homework_1-Qiskit-Verification.ipynb) stores executed output; the comprehensive sections provide self-contained runnable examples.

### Connections across Problems 1–5

Problem 1's Born rule interprets every later count. Problem 2's basis ordering and controlled maps govern Problems 4–5. Problem 3 explains why Problem 4's counts alone cannot certify equality of coherent states; statevector or phase-sensitive checks matter. Problem 4's wire and bit ordering prevent a false interpretation of Problem 5's printed carry/sum strings. Problem 5's Boolean map is a special reversible basis-state computation inside the same unitary formalism.

### Potential conceptual weaknesses for Ryan to assess

Whether our Bloch-angle descriptions at the poles and the distinction between global and relative phase are precise enough; whether our proof that the full-adder carry's XOR equals OR makes the mutual-exclusivity condition explicit enough; whether our Qiskit classical-bit mapping remains clear when the course ket order and Qiskit print order differ; and whether the full-adder stage is distinguished from a chained ripple-carry circuit. These are checkpoints, not invented errors.

### Concepts most important for later CSCI739 work

Measurement-basis choice and phase sensitivity; tensor/operator order; entanglement versus mere superposition; ideal versus noisy evidence; and explicit circuit objective/observable definitions in the QML2 setting.

### Concepts potentially relevant to future quantum research

These foundations may inform phase-aware measurements, circuit verification, resource/depth estimates, and adaptive quantum-system objectives. **The homework establishes only the mathematical and ideal-simulator results above.** It does not establish performance, correctness, or physical behavior of any external quantum-network or QML research system.

### Genuine question worth discussing with Ryan

The summary labels Problem 5 a “1-bit ripple-carry adder,” while its required subparts and diagrams specify one half-adder and one full-adder stage, and Bonus B explicitly asks for a two-bit ripple-carry implementation. Is a chain of full-adder stages intended only for Bonus B? Our required solution follows the detailed Problem 5 subparts and records this distinction.

## Bonus Problems — complete solutions

**Bonus A — Time-Dependent Schrödinger Dynamics and Quantum Control (15 points).** The pinned source asks for an operator solution under commuting \(H(t)\), proof it solves Schrödinger's equation, proof of unitarity for Hermitian \(H\), evaluation for \(H=\hbar\Omega X\), a real \(\Omega\) giving a swap up to global phase, normalization, and identification of the effective gate. Prerequisites: Hermitian adjoints, matrix exponentials, differential equations, global phase, and the gate/unitarity material above. Learning value: it links ideal gates to controlled Hamiltonian evolution.

**Bonus B — Adding 2+2 on a Quantum Computer (15 points).** The pinned source asks for a two-bit ripple-carry adder using two two-qubit registers and carry, binary preparation of \(a=b=2\), a hand or computational trace to \(4=100_2\), output mapping \((s_0,s_1,c_{out})\) versus Qiskit bit strings, simulation and dominant outcome; hardware is optional. Prerequisites: Problem 5's full-adder stage, chained carry, ancilla/register design, least-significant-bit ordering, and Qiskit readout mapping. Learning value: it extends one-bit logic to a multi-stage arithmetic circuit and forces exact endian bookkeeping.

### Bonus A — derivation by subpart

![Example evolution from |0> under H=$\hbar(\pi/2)X$; the general amplitude-swap result is derived below.](./figures/bonus_a_time_evolution.png)

**Given and find.** The initial state is \(|\psi(0)\rangle=\alpha|0\rangle+\beta|1\rangle\), \(|\alpha|^2+|\beta|^2=1\), and \(i\hbar\partial_t|\psi\rangle=H(t)|\psi\rangle\). The question assumes \([H(t),H(t')]=0\) and asks to validate the exponential propagator, prove unitarity for Hermitian \(H\), specialize to \(H=\hbar\Omega X\), normalize the output, and name its gate.

**(a) Starting principle and proof.** Define \(A(t)=-(i/\hbar)\int_0^tH(\tau)d\tau\). The all-times commutation condition gives \([A(t),A'(t)]=0\), with \(A'(t)=-(i/\hbar)H(t)\). We may therefore differentiate the matrix exponential term by term:

\[
\frac{dU}{dt}=\frac{d e^{A(t)}}{dt}=A'(t)e^{A(t)}=-\frac{i}{\hbar}H(t)U(t).
\]

Multiplying by \(i\hbar\) and applying to \(|\psi(0)\rangle\) gives Schrödinger's equation. At \(t=0\), the integral is zero, so \(U(0)=I\) and the initial condition holds. Without the commutation condition, the ordinary exponential derivative is unjustified; the propagator requires time ordering.

**(b) Unitarity.** For Hermitian \(H(t)\), its integral is Hermitian and \(A^\dagger=-A\). Since \((e^A)^\dagger=e^{A^\dagger}\), \(U^\dagger=e^{-A}\). Thus \(U^\dagger U=UU^\dagger=e^{-A}e^A=I\), preserving all inner products. Independently, from \(U'=-(i/\hbar)HU\),

\[
\frac{d}{dt}(U^\dagger U)=\frac{i}{\hbar}U^\dagger HU-\frac{i}{\hbar}U^\dagger HU=0,
\]

using \(H^\dagger=H\) and \(U(0)=I\). This latter check also applies when a time-ordered propagator is needed.

**(c) Matrix and amplitude evolution.** Here \(H=\hbar\Omega X\), \(X=\begin{pmatrix}0&1\\1&0\end{pmatrix}\), and real \(\Omega\) keeps \(H\) Hermitian. Because \(X^2=I\), even and odd powers of the exponential sum separately:

\[
U(t)=e^{-i\Omega tX}=\cos(\Omega t)I-i\sin(\Omega t)X
=\begin{pmatrix}\cos\Omega t&-i\sin\Omega t\\-i\sin\Omega t&\cos\Omega t\end{pmatrix}.
\]

Consequently \(\alpha(t)=\alpha\cos\Omega t-i\beta\sin\Omega t\) and \(\beta(t)=\beta\cos\Omega t-i\alpha\sin\Omega t\). Set the real \(\Omega=\pi/2\), or more generally \(\pi/2+k\pi\). Then \(U(1)=(-1)^k(-iX)\), which swaps the amplitudes up to global phase. The simplest choice gives \(|\psi(1)\rangle=-i\beta|0\rangle-i\alpha|1\rangle\).

**(d) Normalization.** The output probabilities are \(|-i\beta|^2=|\beta|^2\) and \(|-i\alpha|^2=|\alpha|^2\), totaling 1. This agrees with part (b)'s general proof.

**(e) Gate and physical meaning.** Evolution over the interval implements Pauli \(X\) up to an unobservable global phase. The off-diagonal Hamiltonian coherently mixes computational-basis amplitudes; interaction strength and duration set the rotation angle. This is an ideal closed-system gate, not a calibrated physical pulse.

**Independent numerical check and pitfalls.** The executed notebook checks \(U(t)\), \(U^\dagger U\), and the analytic derivative at \(t=0,0.37,1\), then evolves normalized complex amplitudes \((\sqrt{0.3},i\sqrt{0.7})\). It returns final probabilities \((0.7,0.3)\) and norm 1. Common mistakes are treating global \(-i\) as a measurement change, taking \(\Omega\) complex, or differentiating the exponential without the commutation hypothesis.

### Bonus B — derivation, circuit, and output by subpart

![All 16 two-bit input pairs and their three-bit outputs Cout S1 S0; the orange box marks 2+2=4.](./figures/bonus_b_two_bit_addition.png)

**(a) Register roles and construction.** Use six qubits in written order \((q_0,q_1,q_2,q_3,q_4,q_5)=(a_0,a_1,b_0,b_1,c_1,c_{out})\). Here \(a_0,b_0\) are least significant bits; \(q_4\) starts at zero and carries the low-stage overflow into the high stage, then holds \(s_1\); \(q_5\) starts at zero and holds the final carry. These two work qubits retain the intermediate and final carries at the stage handoff. Apply the Problem 5 half-adder gates CCX\((0,2,4)\), CX\((0,2)\), followed by the full-adder gates CCX\((1,3,5)\), CX\((1,3)\), CCX\((3,4,5)\), CX\((3,4)\), CX\((1,3)\). The first stage's \(q_4\) carry is the second stage's carry input, making this a two-stage ripple.

After the low stage, \(q_2=s_0=a_0\oplus b_0\) and \(q_4=c_1=a_0b_0\). After the high stage, \(q_4=s_1=a_1\oplus b_1\oplus c_1\) and \(q_5=c_{out}=a_1b_1\oplus(a_1\oplus b_1)c_1\). The final CX restores \(q_3=b_1\). All gates are reversible on the full register even though only three outputs are read.

**(b) Input encoding.** Since \(2=10_2\), set \(a_1=b_1=1\) and \(a_0=b_0=0\) with X on \(q_1,q_3\). Both work qubits begin at 0. The course-order input ket is \(|010100\rangle\); each two-qubit input register is written \(|a_0a_1\rangle=|01\rangle\), while Qiskit's indexed-bit display is `10`.

**(c) State trace.** The low stage sees \(0+0\), so \((s_0,c_1)=(0,0)\) and leaves \(|010100\rangle\). The high stage sees \(1+1+0\), so \((s_1,c_{out})=(0,1)\). Gate by gate, CCX\((1,3,5)\) changes \(|010100\rangle\to|010101\rangle\); CX\((1,3)\) changes it to \(|010001\rangle\); the next CCX and CX do nothing because \(q_3=q_4=0\); final CX\((1,3)\) restores \(|010101\rangle\). Reading \((q_2,q_4,q_5)\) gives \((s_0,s_1,c_{out})=(0,0,1)\), or \(c_{out}s_1s_0=100_2=4\).

**(d,f) Simulation and bit ordering.** Measure \(q_2\to c_0=s_0\), \(q_4\to c_1=s_1\), and \(q_5\to c_2=c_{out}\). Qiskit prints \(c_2c_1c_0\), so the expected dominant outcome is `100`. AerSimulator returned `{'100': 1024}` for 1024 shots with seed 739. The notebook also checks every \((a,b)\in\{0,1,2,3\}^2\) by statevector and asserts \(s_0+2s_1+4c_{out}=a+b\) for all 16 pairs. The result is not a hard-coded 2+2 circuit.

**(e) Optional hardware.** No hardware job was submitted; there is no measured noisy-hardware distribution to compare. The simulator outcome verifies the ideal circuit only.

**Theory-to-code map and misconceptions.** The notebook's `ripple2(a,b)` prepares the four input bits with conditional X, applies the two gate stages above, and measures only \((q_2,q_4,q_5)\). The low-stage sum stays on \(q_2\). The intermediate carry on \(q_4\) becomes the high-stage sum after being consumed; treating it as still holding \(c_1\) at the end misreads the circuit. The written ket \(|010101\rangle\) is a six-wire state; `100` is a three-bit measurement record. The notebook supplies complete runnable code and saved output.

## Source Reconciliation and Verification Record

- **Authoritative assignment text:** pinned instructor repository ZIP at commit c489b6d29776cb4213d89e0e3d950d26402e7a8a, file Homework 1/main.tex, plus its half/full-adder diagrams. The two adder diagrams were visually inspected before transcribing gate order.
- **Course foundations:** the four linked CSCI739 references listed in the opening; QML0 supplied the direct mathematics, while QML1 and QML2 supplied qualified later context. The course README and lecture artifact index supplied local-source navigation. No unrelated repository or external research source was used.
- **Executed check:** Qiskit 2.5.2 and Aer 0.17.2, ideal AerSimulator, 1024 shots, seed 739. Statevectors, counts, and assertions are saved in the notebook. Probabilistic Problem 4 counts agree with predicted support/distributions; deterministic Problem 5 cases match exactly. Bonus A's operator, differential equation, and norm checks pass; Bonus B's 2+2 case and all 16 input pairs pass. No hardware run was made.
- **Source wording distinctions:** the Problem 4 figures show H on all three qubits, but (d) explicitly instructs H only on \(q_0\); we use figures' all-H setup only for (e). The Problem 5 summary says “1-bit ripple-carry adder,” while the detailed standard problem requests a one-bit half and full stage; Bonus B asks for a chained two-bit implementation. The pinned TeX logistics retain a “TODO — date/time” placeholder, while the course index records the current assignment due date; no deadline is inferred from the pinned TeX. The QML0 reference records a separate slide/transcript minus-basis discrepancy, which does not enter these five calculations.
- **Unresolved technical question:** Ryan's intended scope of “ripple-carry” in required Problem 5 versus Bonus B, as stated above. No mathematical or simulation disagreement remains in Problems 1–5 or the two solved bonuses.

## Instructor Feedback / Knowledge Corrections

No instructor feedback has been received for this solution. For each later comment, add a dated entry without removing the original derivation:

### Original reasoning

Record the exact claim, equation, circuit, or explanation from this version.

### Ryan's feedback

Record his wording or a faithful attributed summary and the source/date.

### Weakness exposed

Identify the precise conceptual or technical gap; do not infer one from a grade alone.

### Corrected understanding

Derive the corrected result and verify it independently.

### Future implication

State which later course or research reasoning must change and why.

Preserve both the original reasoning and correction history when this section is populated.
