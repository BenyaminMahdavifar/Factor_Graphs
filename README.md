# Factor Graphs — Local Rule Routing

> An interactive explanation of belief propagation: why a network of neighbours following local rules reaches the same answer as a central authority examining every possibility — at a fraction of the cost.

[![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-live-4f8eff?style=flat-square&logo=github)](https://benyaminmahdavifar.github.io/Factor_Graphs/docs/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)
[![Notebook](https://img.shields.io/badge/Jupyter-notebook-orange?style=flat-square&logo=jupyter)](Factor_Graphs.ipynb)

---

## Overview

**Key analogy:**

- **Martial law** — a central command collects all information, examines every possible configuration, and issues one global order. Equivalent to direct enumeration of the joint distribution.
- **Local police / urban traffic control** — each officer only talks to neighbours and enforces a simple local rule. Global order emerges from these local interactions. Equivalent to a **factor graph**.

This repository breaks a global function into local **factors**, and shows that passing messages between neighbours yields the exact same answer as brute-force enumeration — without ever building the full joint table.

---

## Live Dashboard

**[benyaminmahdavifar.github.io/Factor_Graphs/docs/](https://benyaminmahdavifar.github.io/Factor_Graphs/docs/)**

### Interactive sections

| Section | What you can do |
|---|---|
| **Triangle graph** | Click any of the three pairwise factors and drag its bias slider — the global joint table and marginals update live |
| **Traffic light chain** | Toggle each local rule between "prefer same" / "prefer opposite", then step through forward and backward message passing one message at a time |
| **Complexity** | Drag n from 2 to 40 and watch direct enumeration (2ⁿ) explode while message passing (2n) stays flat |
| **Intuition** | Side-by-side martial-law vs. local-police framing with the four core ideas of belief propagation |

---

## Key Results

| Quantity | Direct computation | Factor graph |
|---|---|---|
| States enumerated | 2ⁿ | never built explicitly |
| Per-node cost | grows exponentially | O(1) per neighbour |
| Total operations (chain) | 2ⁿ | 2n |
| Scalability beyond n ≈ 30 | infeasible | unaffected |

For a chain of *n* binary variables, message passing computes the exact marginal or MAP assignment using only `2n` operations — compared to `2ⁿ` for brute-force enumeration.

$$F(x_1,\dots,x_n) = \prod_i f_i(\text{neighbours of } i)$$

---

## Notebook

`Factor_Graphs.ipynb` contains:

- A 3-variable triangle example comparing direct computation (8 states) vs. three local 2×2 factor tables
- A hand-simulated sum-product message passing routine
- A 4-intersection traffic-light chain solved by both brute force and max-product (Viterbi-style) message passing
- A complexity comparison plot: 2ⁿ vs. 2n as n grows from 2 to 12

### Run locally

```bash
git clone https://github.com/BenyaminMahdavifar/Factor_Graphs.git
cd Factor_Graphs
pip install numpy matplotlib networkx jupyter
jupyter notebook Factor_Graphs.ipynb
```

---

## Repository structure

```
├── docs/
│   └── index.html          # Interactive dashboard (GitHub Pages)
├── index.html               # Root redirect → docs/
├── Factor_Graphs.ipynb      # Full notebook with simulations
└── README.md
```

---

## GitHub Pages setup

1. Go to **Settings → Pages**
2. Set Source to **main** branch, folder **/ (root)**
3. Save — the site is live in ~60 seconds

---

## Author

**Benyamin Mahdavifar** · [github.com/BenyaminMahdavifar](https://github.com/BenyaminMahdavifar)
