# PyCon Aviation Puzzle

Solution to the [Gurobi PyCon 2026 Aviation Challenge](https://colab.research.google.com/github/Gurobi/gurobi-event-material/blob/main/events/2026-04-pycon/pycon_aviation_puzzle.ipynb) -- a tail assignment optimization problem.

## The Problem

Assign 16 flights (across airports A-D) to 4 airplanes, each with different hourly operating costs and starting airports. The goal is to minimize total operating cost while respecting:

- Each airplane's first flight must depart from its starting airport
- Consecutive flights must connect (arrival airport = next departure airport)
- No time overlaps (arrival time <= next departure time)
- Every flight must be covered exactly once

## The Solution

The problem is modeled as a Mixed-Integer Program (MIP) and solved with Gurobi to provable optimality (0% MIP gap).

| Airplane | Cost/hr | Start | Flights | Schedule Cost |
|----------|---------|-------|---------|---------------|
| A1 | $4,000 | A | GRB01 -> GRB06 -> GRB15 -> GRB09 | $40,000 |
| A2 | $6,000 | B | GRB05 -> GRB12 -> GRB03 -> GRB13 | $69,000 |
| A3 | $8,000 | C | GRB10 -> GRB07 -> GRB04 -> GRB08 | $68,000 |
| A4 | $10,000 | D | GRB14 -> GRB11 -> GRB02 -> GRB16 | $80,000 |

**Optimal total cost: $257,000**

The cheapest airplane (A1) flies the most hours (10h), while the most expensive (A4) flies the fewest (8h). The solver proves no valid assignment exists below this cost.

## Setup

Requires Python 3.13 and [uv](https://docs.astral.sh/uv/):

```bash
uv sync
uv run jupyter execute pycon_aviation_puzzle.ipynb
```
