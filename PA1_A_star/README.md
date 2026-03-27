# PA3-A – A\* Search Algorithm (8-Puzzle)

**Course:** AI201 – Artificial Intelligence
**Semester:** 2nd Semester, AY 2025–2026
**Instructor:** Prospero C. Naval, Jr., Ph.D.
**Author:** Adriane Jone A. Abunda (2025-22450)
**Due Date:** February 20, 2026

---

## Overview

This assignment implements the **A\* informed search algorithm** to solve the classic **8-puzzle problem** — a 3×3 sliding tile puzzle where the goal is to reach a target configuration from a given start state by sliding tiles into the blank space.

The implementation strictly follows the A\* pseudocode from Lecture 3B of the course, using explicit `OPEN` and `CLOSED` lists. Three heuristic functions of increasing complexity are compared to evaluate their effect on search efficiency.

All logic is implemented in pure Python (no external libraries beyond standard I/O).

---

## The 8-Puzzle Problem

The board is a 3×3 grid containing tiles numbered 1–8 and a blank space (`*`). A move consists of sliding an adjacent tile into the blank. The task is to find the **optimal sequence of moves** from a given start state to the goal state.

```
Start State        Goal State
+---+---+---+     +---+---+---+
| 2 | 8 | 3 |     | 1 | 2 | 3 |
+---+---+---+     +---+---+---+
| 1 | 6 | 4 |     | 8 | * | 4 |
+---+---+---+     +---+---+---+
| 7 | * | 5 |     | 7 | 6 | 5 |
+---+---+---+     +---+---+---+
```

---

## Algorithm

The A\* algorithm estimates the total path cost for each node as:

```
f(n) = g(n) + h(n)
```

Where:
- `g(n)` — actual cost from the start node to node `n` (number of moves taken)
- `h(n)` — heuristic estimate of the remaining cost to the goal
- `f(n)` — total estimated cost through node `n`

The algorithm expands the node with the lowest `f(n)` first, guaranteeing an **optimal solution** when the heuristic is admissible (never overestimates the true cost).

---

## Heuristic Functions

### a) Misplaced Tiles
Counts the number of tiles that are not in their goal position (excluding the blank). A simple but weak heuristic — it does not account for how *far* each tile needs to travel.

### b) Manhattan Distance
Sums the horizontal and vertical distances of each tile from its goal position. More informative than Misplaced Tiles because it reflects the actual effort needed to move each tile.

```
h(n) = Σ |row_current - row_goal| + |col_current - col_goal|   for all tiles ≠ blank
```

### c) Nilsson's Sequence Score
The most informative heuristic. Combines Manhattan distance with a **sequence score** that penalizes tiles that are out of their correct clockwise order around the center:

```
h(n) = P(n) + 3 × S(n)
```

Where:
- `P(n)` — Manhattan distance of all tiles
- `S(n)` — sequence score: +2 for each edge tile not followed by its correct successor, +1 if the center tile is not blank

---

## Files

| File | Description |
|---|---|
| `AI201-2S2025-26-PA_1 Astar.pdf` | Instructions for the assignment |
| `AI201_Programming_Assignment_1.ipynb` | Main Jupyter Notebook (all cells pre-executed) |
| `astar_in.txt` | Input file containing the start and goal states |

---

## Input Format

The puzzle states are read from `astar_in.txt`. The file uses `start` and `goal` as section headers, with tiles listed row by row. The blank tile is represented as `*`.

```
start
2 8 3
1 6 4
7 * 5
goal
1 2 3
8 * 4
7 6 5
```

---

## How to Run

1. Ensure Python 3 is installed.
2. Place `AI201_Programming_Assignment_1.ipynb` and `astar_in.txt` in the same directory.
3. Open the notebook in Jupyter and run all cells.

The notebook will print the complete solution path for each heuristic, including the board state and `f(n)`, `g(n)`, `h(n)` values at each step. For Nilsson's Sequence Score, `P(n)` and `S(n)` are also displayed. The total number of nodes generated is printed at the end of each run.

> All cells are pre-executed with outputs visible.

---

## Key Findings

The three heuristics demonstrate a clear progression in search efficiency. More informative heuristics guide the algorithm toward the goal more directly, generating fewer unnecessary nodes. Nilsson's Sequence Score consistently achieves the lowest node count by incorporating sequence ordering constraints that neither Misplaced Tiles nor Manhattan Distance capture. This validates the theoretical principle that a more informed heuristic leads to a more efficient A\* search.

---

## Key Concepts Demonstrated

- Informed search and the A\* algorithm
- Heuristic admissibility and consistency
- OPEN/CLOSED list management
- State-space representation of combinatorial puzzles
- Heuristic comparison and search efficiency analysis
