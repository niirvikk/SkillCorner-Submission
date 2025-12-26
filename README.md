# SkillCorner-Submission

# Quantum Optimisation for Football Passing Decisions

This project explores how football passing decisions can be formulated as explicit optimisation problems and solved using quantum methods. Instead of learning pass preferences from historical data, each on-ball decision is evaluated directly based on the spatial configuration of play.

The core contribution is a decision-level framework that identifies optimal passing options, evaluates real player decisions against this optimum, and enables interpretable analysis of decision behaviour.

---

## Problem Overview

At each decision moment in a football match, the ball carrier faces multiple feasible passing options, each with different spatial and tactical trade-offs. Selecting the best pass is a combinatorial problem that depends on player positioning, direction of play, and risk.

Most existing approaches rely on supervised learning to rank passes based on historical outcomes. While effective in common situations, such methods do not explicitly solve the underlying decision problem and can struggle to generalise to uncommon spatial configurations.

This project instead treats each decision as an optimisation task, solved independently using a simple, interpretable objective.

---

## Methodology

Each on-ball decision is processed as follows:

1. **Candidate generation**  
   Viable passing options are identified using football-realistic constraints:
   - The receiver must be a teammate
   - The receiver must not be the ball carrier
   - The pass must lie within a practical distance range

2. **Pass valuation**  
   Each candidate pass is assigned a continuous value score based on:
   - Forward progression relative to the attacking direction
   - Effective distance, rewarding medium-range progressive passes

3. **Optimisation formulation**  
   Scores are normalised and encoded into a Quadratic Unconstrained Binary Optimisation (QUBO) objective, where selecting exactly one pass corresponds to the optimal decision.

4. **Decision evaluation**  
   Quantum optimisation is used to identify high-quality passing options. Decisions are compared against the brute-force optimum using decision-centric metrics.

---

## Decision Metrics

Two lightweight metrics are used to evaluate decision quality:

- **Decision Efficiency Score (DES)**  
  Measures how close the selected pass is to the QUBO-optimal pass.

- **Quantum Evaluation Score (QES)**  
  Measures how strongly the selected pass is favoured by the quantum solution.

These metrics enable consistent comparison across decision moments without relying on outcome-based labels.

---

## Results

- Quantum optimisation consistently outperforms machine-learning baselines in recovering optimal passing decisions.
- Player-level decision statistics naturally separate players into interpretable decision-style groups, such as *Optimal / Efficient*, *Conservative / Safe*, and *Inefficient / Risky*.
- Detailed walkthroughs demonstrate how individual football decisions are transformed into optimisation problems and evaluated end to end.

---

## Repository Structure

- **submission.py** contains the final submission logic and is the primary artefact evaluated.
- **All data** required to run the project is stored under `src/data`.
- **explanation.ipynb** provides a detailed, line-by-line walkthrough of the entire codebase and includes the full Dirac-3 implementation.

---

## Reproducibility Notes

- All optimisation logic and evaluation code are fully reproducible.
- Quantum Approximate Optimisation Algorithm (QAOA) results are obtained using open-source implementations.
- The Dirac-3 implementation is included for completeness and can be run by any user who obtains API access from Quantum Computing Inc. (QCI). Basic API access is available directly from QCI.


---

## Extensions

While this work focuses on passing decisions, the same optimisation framework can be extended to other football actions, such as:
- Shot selection
- Ball progression decisions
- Defensive positioning and marking

More broadly, the approach highlights quantum optimisation as a promising direction for structured decision-making problems in sports analytics.

---

## Acknowledgements

This project was developed as part of SkillCorner x PySport hackathon and builds on publicly available football tracking and event data.
