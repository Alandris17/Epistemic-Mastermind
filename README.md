# MastersMinds: Epistemic Logic and Information Theory

**MastersMinds** is a competitive two-sided variant of the classic Mastermind game. This project models the game as an epistemic interaction where every guess is a **public announcement**: you learn about the opponent’s code while simultaneously leaking information about your own.

---

## Quick Start: View the Report

The project documentation and experimental results are served as an interactive web report. To view it locally:

1.  **Open your terminal** in the project root directory.
2.  **Start a local server**:
    ```bash
    python -m http.server 8000
    ```
3.  **View in your browser**:
    Navigate to [http://localhost:8000/index.html](http://localhost:8000/index.html)

---

## Game Overview

We use a simplified version of Master(s)Mind(s) to ensure a computationally feasible state space:
* **Code Length**: 3 slots (no repeated colors).
* **Colors**: 5 available (Red, Blue, Yellow, Green, Pink).
* **State Space**: Initially consists of $60 \times 60 = 3600$ possible worlds (code-pairs).
* **Public Feedback**: Each guess produces two feedback values (black/white pins) comparing the guess against both the opponent's and the guesser's secret codes.
* **Victory Condition**: Focuses on **Epistemic Success**—the moment a player's internal Kripke model collapses to a single possible code for the opponent.

---

## Theoretical Framework

The project utilizes **Dynamic Epistemic Logic (DEL)** and **Public Announcement Logic (PAL)** to track knowledge changes:

* **Kripke Models**: States are represented as ordered pairs $(\text{code}_i, \text{code}_j)$ with $S5$ indistinguishability relations.
* **PAL Updates**: Feedback acts as a public announcement formula $\mathsf{Ann}(g,o)$, restricting the Kripke model to states consistent with the observed pins.
* **Higher-Order Knowledge**: Because announcements are public, agents can reason about what the opponent knows that they know.

---

## Strategies

We implement three strategy classes grounded in information-theoretic measures (Hartley entropy):

1.  **Guessing-focused**: Solely maximizes expected Information Gain ($IG$) about the opponent.
2.  **Hiding-focused**: Solely minimizes Information Leakage ($IL$) about the agent's own secret.
3.  **Balanced ($\lambda$)**: Uses a trade-off parameter $\lambda$ to maximize a utility function:
    $$U_i(g) = \mathrm{IG}_i^{\mathit{opp}}(g) - \lambda \cdot \mathrm{IL}_i(g)$$
    $\lambda$ represents how many bits of self-leakage an agent tolerates for one bit of information gain.

---

## Experimental Results

A round-robin tournament of 280 games was conducted to evaluate performance:

* **Efficiency**: Convergence is rapid, with games terminating in an average of **1.79 rounds**.
* **Symmetry**: **79.6%** of games resulted in a **tie** (mutual epistemic success), confirming that public announcements collapse belief states for both players simultaneously.
* **Strategy Impact**: Higher $\lambda$ values lead to more conservative play, slightly increasing the number of rounds to termination while preserving secrecy.

---

**Software Stack**: Python (Engine/Experiments), HTML/CSS (Report/Layout), MathJax (Notation).
