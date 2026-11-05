# Simulated Annealing for the Traveling Salesman Problem

An animation of simulated annealing solving the Traveling Salesman Problem (TSP) on a map of random cities. It shows random swaps being accepted or rejected, with live graphs of temperature and tour length.

**To run:** open `tsp_annealing.html` in a web browser and press Start.

## Theory

### Traveling Salesman Problem (TSP)

Given *n* cities, find the shortest closed route that visits every city exactly once and returns to the start. The number of possible tours grows as (n − 1)! / 2, so checking all of them is impossible for even a moderate number of cities. TSP is NP-hard, so heuristics are used to find good tours.

### Simulated Annealing

Simulated annealing is inspired by annealing in metallurgy: a metal is heated and then cooled slowly so it settles into a low-energy state.

| Annealing | TSP |
|-----------|-----|
| Energy | Tour length |
| Temperature (T) | Willingness to accept worse tours |
| Slow cooling | T ← α · T (α slightly below 1) |

A plain "keep only improvements" search gets stuck in local minima. Simulated annealing avoids this by sometimes accepting a worse tour, and it does so less often as the temperature drops.

## How it solves TSP

1. Start with a random tour and a high temperature T.
2. **Random swap (2-opt):** pick two random positions and reverse the part of the tour between them. This removes two edges and adds two new ones.
3. Compute the change in length: Δ = new length − old length.
4. **Accept or reject:**
   - If Δ < 0 (shorter tour), accept.
   - Otherwise, accept with probability **p = e^(−Δ/T)**. Pick a random number r in [0, 1). If r < p, accept; otherwise reject and keep the old tour.
5. Cool down: T ← α · T.
6. Repeat from step 2 until T is very small. The best tour found is the answer.

**What happens over time**

- **High T:** p is close to 1, so almost every move is accepted, even bad ones. The tour looks random and its length goes up and down.
- **Low T:** p is close to 0, so only improving moves are accepted. The tour settles into a short route with no crossing edges.

## What the animation shows

- **Green edges:** new edges after an accepted swap.
- **Red dashed edges:** edges of a rejected swap.
- **Grey dashed edges:** edges removed by an accepted swap.
- **Temperature graph:** falls steadily as the tour cools.
- **Tour length graph:** current length (noisy at first, then steady) and best length so far.
