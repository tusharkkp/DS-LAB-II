# DS-LAB-II — Data Structures & Algorithms in C++

**A verified, hand-built collection of C++ console programs implementing core data structure and algorithm concepts — hash tables, deques, CPU scheduling, backtracking, and sorting/searching — from a Data Structures Laboratory course.**

![Top Language](https://img.shields.io/github/languages/top/tusharkkp/DS-LAB-II)
![License](https://img.shields.io/github/license/tusharkkp/DS-LAB-II)
![Build Status](https://github.com/tusharkkp/DS-LAB-II/actions/workflows/build.yml/badge.svg)
![Last Commit](https://img.shields.io/github/last-commit/tusharkkp/DS-LAB-II)
![Repo Size](https://img.shields.io/github/repo-size/tusharkkp/DS-LAB-II)

> **Note on badges:** the License and Build badges will render correctly once the `LICENSE` file and `.github/workflows/build.yml` in this delivery are added to the live repository. They are dynamic (pulled live from GitHub), not static claims.

---

## Table of Contents

- [Overview](#overview)
- [Why This Repository Exists](#why-this-repository-exists)
- [What's Implemented](#whats-implemented)
- [Verified Build & Run Status](#verified-build--run-status)
- [Getting Started](#getting-started)
- [Example Run (Verified Output)](#example-run-verified-output)
- [Repository Structure](#repository-structure)
- [Tech Stack](#tech-stack)
- [Algorithmic Concepts & Complexity](#algorithmic-concepts--complexity)
- [API Documentation](#api-documentation)
- [Environment Variables](#environment-variables)
- [Performance Notes & Known Limitations](#performance-notes--known-limitations)
- [Future Scope](#future-scope)
- [Contributing](#contributing)
- [License](#license)
- [Author](#author)

---

## Overview

This repository is a collection of **eight standalone, menu-driven C++ programs**, each implementing a specific data structure or algorithm assigned as a practical exercise in a Data Structures Laboratory (DS Lab II) course. Every program is self-contained — it compiles independently with a single `g++` command and runs as an interactive command-line application.

This is a **console-program collection, not a web app or service**. There is no frontend, backend, database, or API in this repository, and this README does not claim otherwise.

## Why This Repository Exists

*(Inferred from repository content and naming conventions — not an explicit repo description.)* The file names (`practical 10.cpp`, `Practical 11(a/b/c).cpp`) map directly to numbered lab assignments, suggesting this repo serves as:
- A working record of completed DS Lab practicals.
- A revision reference for exams, viva questions, and technical interviews on hash tables, queues, scheduling, and backtracking.
- A portfolio artifact demonstrating hands-on C++ and algorithmic problem-solving.

## What's Implemented

| # | Program | Core Concept | File |
|---|---------|---------------|------|
| 1 | Double-Ended Queue (Deque) | Input-restricted & output-restricted deque, singly linked list | `Dequeue.cpp` |
| 2 | Hash Table — Linear Probing | Collision resolution without replacement (table size 6) | `Practical 11(a).cpp` |
| 3 | Hash Table — Separate Chaining | Linked-list buckets (table size 20) | `Practical 11(b).cpp` ⚠️ see below |
| 4 | Hash Table — Quadratic Probing | Collision resolution without replacement (table size 11) | `Practical 11(c).cpp` |
| 5 | Round Robin CPU Scheduling | Simulated via a custom circular queue; prints Gantt chart, waiting/turnaround time | `RR.cpp` |
| 6 | Sudoku Solver (4×4) | Recursive backtracking over 2×2 sub-grids, user-supplied puzzle | `Sudoku 2x2.cpp` |
| 7 | Sudoku Solver (9×9) | Recursive backtracking over 3×3 sub-grids, hardcoded puzzle | `Sudoku 3x3.cpp` |
| 8 | Student Record Management System | Bubble/Insertion/Quick sort + Linear/Binary/Fibonacci search over a struct array | `practical 10.cpp` |

Each program has its own interactive `cin`-driven menu (except the 9×9 Sudoku solver and the two pre-populated hash table demos, which run on built-in sample data).

**Not present in this repository** (flagged here rather than assumed): linked lists, stacks, trees, graphs, heaps, or shortest-path/MST algorithms are not implemented here, despite appearing in an earlier draft of this README. See [Future Scope](#future-scope).

## Verified Build & Run Status

Every file in this repository was compiled with `g++ (Ubuntu 13.3.0) -std=c++17 -Wall -Wextra` and run with sample input as part of this documentation update:

| File | Compiles? | Runs as expected? |
|------|:---:|:---:|
| `Dequeue.cpp` | ✅ | ✅ Verified (insert/delete front & rear) |
| `Practical 11(a).cpp` | ✅ | ✅ Verified (linear probing, 5 sample keys) |
| `Practical 11(b).cpp` | ❌ **Fails to compile** | — see [Known Issue](#performance-notes--known-limitations) |
| `Practical 11(c).cpp` | ✅ (2 minor warnings) | ✅ Verified (quadratic probing, 11 sample keys) |
| `RR.cpp` | ✅ | ✅ Verified (3-process schedule, quantum 2) |
| `Sudoku 2x2.cpp` | ✅ | ✅ Verified (4×4 puzzle solved correctly) |
| `Sudoku 3x3.cpp` | ✅ | ✅ Verified (9×9 puzzle solved correctly) |
| `practical 10.cpp` | ✅ | ✅ Verified (sort/search menu, 3 sample records) |

## Getting Started

### Prerequisites
- A C++ compiler: GCC/G++ (recommended) or Clang
- A terminal / shell

### Clone
```bash
git clone https://github.com/tusharkkp/DS-LAB-II.git
cd DS-LAB-II
```

### Compile & Run

Several filenames contain spaces and parentheses — **quote the filename** when compiling:

```bash
g++ -o dequeue Dequeue.cpp && ./dequeue
g++ -o roundrobin RR.cpp && ./roundrobin
g++ -o sudoku4x4 "Sudoku 2x2.cpp" && ./sudoku4x4
g++ -o sudoku9x9 "Sudoku 3x3.cpp" && ./sudoku9x9
g++ -o studentmgmt "practical 10.cpp" && ./studentmgmt
g++ -o hash_linear "Practical 11(a).cpp" && ./hash_linear
g++ -o hash_quadratic "Practical 11(c).cpp" && ./hash_quadratic
```

> ⚠️ `Practical 11(b).cpp` (separate chaining) currently **fails to compile** — see the fix below.

## Example Run (Verified Output)

**4×4 Sudoku solver**, given a partially filled puzzle:

```
Enter 4x4 Sudoku puzzle (use 0 = empty cells):

Initial Sudoku:
+-----+-----+
| 1 0 | 0 4 |
| 0 0 | 1 0 |
+-----+-----+
| 0 1 | 0 0 |
| 4 0 | 0 1 |
+-----+-----+

Solved Sudoku:
+-----+-----+
| 1 2 | 3 4 |
| 3 4 | 1 2 |
+-----+-----+
| 2 1 | 4 3 |
| 4 3 | 2 1 |
+-----+-----+
```

**Round Robin scheduling** (3 processes, quantum = 2):

```
Gantt Chart (Process Execution Order):
| P1 | P2 | P3 | P1 | P2 | P3 | P1 | P3 | P3 |

Process AT  BT  CT  TAT WT
P1      0   5   12  12  7
P2      1   3   9   8   5
P3      2   8   16  14  6

Average Waiting Time: 6
Average Turnaround Time: 11.3333
```

## Repository Structure

```
DS-LAB-II/
├── Dequeue.cpp
├── Practical 11(a).cpp
├── Practical 11(b).cpp
├── Practical 11(c).cpp
├── RR.cpp
├── Sudoku 2x2.cpp
├── Sudoku 3x3.cpp
├── practical 10.cpp
└── README.md
```

All eight programs currently live as a flat file list in the repository root. There are **no** `Linear/`, `NonLinear/`, `Algorithms/`, or `Assignments/` subfolders — an earlier version of this README described that structure, but it does not exist in the actual repository. This document reflects only what is verifiably present.

## Tech Stack

| Layer | Technology | Why |
|---|---|---|
| Language | C++ (C++17-compatible) | Required by the lab course; gives direct control over pointers/memory for teaching data structures |
| Compiler | GCC / G++ | Free, ubiquitous, standard for academic C++ | 
| Build | Manual `g++` per-file compilation | No build system is currently configured (see [Future Scope](#future-scope)) |
| Dependencies | None — C++ Standard Library only (`<iostream>`, `<bits/stdc++.h>`) | Keeps every file trivially portable and dependency-free |

There is no frontend, backend, database, or deployment pipeline in this repository.

## Algorithmic Concepts & Complexity

Complexity of the algorithms actually implemented in this repository:

| Structure / Algorithm | Where | Time Complexity |
|---|---|---|
| Deque insert/delete (front or rear) | `Dequeue.cpp` | O(1) |
| Hash table insert/lookup (average case) | `Practical 11(a/b/c).cpp` | O(1) average, O(n) worst case under heavy collisions |
| Bubble Sort | `practical 10.cpp` | O(n²) |
| Insertion Sort | `practical 10.cpp` | O(n²) |
| Quick Sort (average / worst) | `practical 10.cpp` | O(n log n) average, O(n²) worst case |
| Linear Search | `practical 10.cpp` | O(n) |
| Binary Search | `practical 10.cpp` | O(log n) — requires pre-sorted data (handled in code) |
| Fibonacci Search | `practical 10.cpp` | O(log n) — requires pre-sorted data (handled in code) |
| Round Robin scheduling | `RR.cpp` | O(n · ⌈burst/quantum⌉) |
| Sudoku backtracking (4×4 / 9×9) | `Sudoku 2x2.cpp` / `Sudoku 3x3.cpp` | Exponential worst case; fast in practice due to constraint pruning |

## API Documentation

**Not found in repository.** This project has no HTTP API, RPC interface, or client-server component of any kind. If a reusable library interface is ever desired, see [Future Scope](#future-scope).

## Environment Variables

**Not applicable.** None of the eight programs read environment variables or configuration files — all input is supplied interactively via `cin` (or, for two programs, hardcoded sample arrays). No `.env.example` is included because there is nothing for it to document.

## Performance Notes & Known Limitations

- **🐛 Known issue — `Practical 11(b).cpp` does not compile.** The `Node` class declares `data` and `next` without an access specifier, so both default to `private`. `main()` then accesses `newNode->data` and `newNode->next` directly, which GCC correctly rejects. **Verified one-line fix:** change `class Node {` to `struct Node {` (structs default to public), or add an explicit `public:` label. A corrected copy is included in this delivery at `fixes/Practical 11(b) - fixed.cpp` — verified to compile and run correctly.
- **Quadratic probing table-full behavior (`Practical 11(c).cpp`):** with the built-in 11-key sample dataset inserted into an 11-slot table, one key fails to insert (`Table full!`) even though the table is not logically full. This is expected, textbook behavior of quadratic probing at high load factor, not a bug — worth calling out explicitly if this is demonstrated live (e.g., in a viva).
- **Fixed-size storage:** `practical 10.cpp` uses a fixed `Student s[100]` array and `RR.cpp` uses `#define MAX 50` — both cap the dataset size and would need to move to `std::vector` to scale further.
- **No input validation:** most programs trust that the user enters well-formed integers/strings; malformed input (e.g., letters where a number is expected) is not handled.

## Future Scope

Everything below is a **recommendation or possible improvement — none of it currently exists in the repository:**

- Implement the classic structures an earlier README implied but that aren't here yet: linked lists, stacks, binary search trees/AVL trees, graphs (BFS/DFS), Dijkstra, Prim/Kruskal MST, heaps.
- Refactor raw arrays/manual pointers to STL containers (`std::vector`, `std::unordered_map`, `std::deque`) as a "modern C++" companion version of each practical.
- Add a unit test suite (e.g., Catch2 or GoogleTest) per algorithm.
- Add a `CMakeLists.txt` or `Makefile` to replace manual per-file `g++` invocations.
- Consistent file naming — see the audit report for a concrete renaming proposal.
- Doxygen-style documentation comments for each class/function.
- A single umbrella CLI that lets a user pick any of the 8 practicals from one entry point.

## Contributing

See [`CONTRIBUTING.md`](CONTRIBUTING.md) for how to propose changes, report bugs, or add new practicals.

## License

Recommended: **MIT License** (see [`LICENSE`](LICENSE)). No license was present in the original repository; the previous README only stated an informal "for educational purposes" note, which is not a substitute for a real open-source license.

## Author

**Tushar Kaldate**
GitHub: [@tusharkkp](https://github.com/tusharkkp)

*(No LinkedIn or portfolio link was found in the repository — add one here if you'd like it surfaced to recruiters.)*
