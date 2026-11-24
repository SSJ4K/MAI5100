# HW0 Written Answers

**Name: Shaquan Antone Giddings**
**Student ID: 1037224**

---

## Part B: Written Problems

### B1. State spaces and uninformed search

1.![state_diagram.jpeg](../../../../Downloads/state_diagram.jpeg)

<br>
<br>

2. <br>BFS: 1 -> 2 -> 3 -> 4 -> 5 -> 6 -> 7 -> 8 -> 9 -> 10 -> 11<br>
    DFS limit = 3: 1 -> 2 -> 4 -> 5 -> 3 -> 6 -> 7 <br>
    Iterative Deepening: 1 -> 1 -> 2 -> 3 -> 1 -> 2 -> 4 -> 5 -> 3 -> 6 -> 7 -> 1 -> 2 -> 4 -> 8 -> 9 -> 5 -> 10 -> 11<br>

3. <br>Bidirectional search would solve this problem rather quickly, as the nodes expadning from the start state would join the ones coming from the gol state at around two levels. Whether or not this path is the best path is of no concern to the joining function, but that of a terminating function.<br>The branching factors moving forward are the two child nodes, and each node has one parent node making that the branching factor going backwards.<br><br>
4. <br>1. writing the goal (g) in binary<br> 2. Remove the leading 1<br>3. Read the remaining bits as actions<br><br>Regarding the value of a good problem formulation, we can see that in trimming unnecessary data the actions needed for an agent to reach its goal becomes much clearer.

### B2. Problem formulation and heuristics

1. <br> number of squares: n * n = n<sup>2</sup><br>
   vehicle 2 and one can't occupy same space, and their squares are alredy occupied by them so we have: n<sup>2</sup> - 2 choices<br>
   multiply for each vehicle:n<sup>2</sup> ( n<sup>2</sup> - 1 ) ( n<sup>2</sup> - 2 ) ... (n<sup>2</sup> - n + 1 )<br>
   state space: ( n<sup>2</sup> )! / ( n<sup>2</sup> - n ) !<br><br>
2. Each vehicle has five options (up, down, left, right, still). The branching factor is therefore 5<sup>n</sup><br><br>
3.  h<sub>i</sub> = |(n - i  1) - x | + |n - y|<br><br>
4. (a): this is not admissible because the vehicles move in parllel nd n vehicles can cut their distance by 1 in one step.<br><br> (b): this is also not admissible because hopping lets a vehicle cover 2 squares in one step<br><br> (c): this is admissible because when a vehicle moves normally its h<sub>i</sub> is reduced by at most 1, if a vehicle hops it's reduced by at most 2, and each hop needs its own vehicle staying put because at most 1 vehicle can hop over a given vehicle. That staying vehicle reduces its hᵢ by 0.


### B3. Proofs about heuristics

1.<br>heuristic is consistent for every node n and successor n': h(n)<= c (n, n') + h(n')<br> apply consistency rule: h(n<sub>0</sub>) <= c(n<sub>0</sub>, <sub>1</sub>) + h(n<sub>1</sub>)     h(n<sub>1</sub>) <= c(n<sub>1</sub>, n<sub>2</sub>) + h(n<sub>2</sub>) 
<br> h(n<sub>0</sub>) <= c(n<sub>0</sub>, n<sub>1</sub>)  + c(n<sub>1</sub>, n<sub>2</sub>) + ...  c(n<sub>k-1</sub>, n<sub>k</sub>) + h(n<sub>k</sub>)<br>
heuristic gol is 0: h(n<sub>k</sub>) = 0<br>
therefore: h(n<sub>0</sub>) <= <sup>k-1</sup>∑<sub>i = 0</sub> c(n<sub>i</sub>, n<sub>i+1</sub>)<br>
thus: h(n) <= h<sup>*</sup>(n)   proving that h is admissible<br><br>
2.<br>
   h<sub>1</sub> and h<sub>2</sub> are admissible: h<sub>1</sub>(n) <= h<sup>*</sup>(n) and h<sub>2</sub>(n) <= h<sup>*</sup>(n) for every n<br>
   h(n) = max(h<sub>1</sub>(n), h<sub>2</sub>(n)) is always equal to either h<sub>1</sub>(n) or h<sub>2</sub>(n), and both are <= h<sup>*</sup>(n)<br>
   therefore: h(n) <= h<sup>*</sup>(n) for every n, proving that max(h<sub>1</sub>, h<sub>2</sub>) is admissible<br><br>
   h<sub>1</sub>(n) + h<sub>2</sub>(n) is not admissible in general, counterexample:<br>
   two nodes S and G (goal), one edge S → G with cost 1, so h<sup>*</sup>(S) = 1<br>
   let h<sub>1</sub>(S) = h<sub>2</sub>(S) = 1 and h<sub>1</sub>(G) = h<sub>2</sub>(G) = 0, both are admissible since they equal the true cost<br>
   h<sub>1</sub>(S) + h<sub>2</sub>(S) = 1 + 1 = 2 > 1 = h<sup>*</sup>(S)<br>
   the sum overestimates the true cost, so h<sub>1</sub> + h<sub>2</sub> is not admissible<br><br>
3.<br>
   weighted A*: f(n) = g(n) + w · h(n), with w > 1 and h admissible: h(n) <= h<sup>*</sup>(n) and h(goal) = 0<br>
   let C<sup>*</sup> be the optimal cost and n<sub>0</sub>, n<sub>1</sub>, ..., n<sub>m</sub> be an optimal path from start to goal<br>
   until a goal is expanded, some node n<sub>i</sub> on the optimal path is always in the frontier (n<sub>0</sub> starts there, and expanding n<sub>i</sub> adds n<sub>i+1</sub>)<br>
   n<sub>i</sub> was reached along the optimal path, so: g(n<sub>i</sub>) + h<sup>*</sup>(n<sub>i</sub>) = C<sup>*</sup><br>
   f(n<sub>i</sub>) = g(n<sub>i</sub>) + w · h(n<sub>i</sub>) <= g(n<sub>i</sub>) + w · h<sup>*</sup>(n<sub>i</sub>) (h is admissible)<br>
   g(n<sub>i</sub>) + w · h<sup>*</sup>(n<sub>i</sub>) <= w · g(n<sub>i</sub>) + w · h<sup>*</sup>(n<sub>i</sub>) = w · C<sup>*</sup> (w > 1 and g >= 0)<br>
   so: f(n<sub>i</sub>) <= w · C<sup>*</sup><br>
   when the search picks a goal G to expand, n<sub>i</sub> is still in the frontier, so: f(G) <= f(n<sub>i</sub>)<br>
   h(G) = 0, so: cost(G) = g(G) = f(G) <= f(n<sub>i</sub>) <= w · C<sup>*</sup><br>
   thus: the solution returned costs at most w times the optimal cost<br><br>
   why accept a suboptimal answer: <br> 1. Faster execution: weighted A<sup>*</sup> can find solutions more quickly.<br>2. Less computation: may explore fewer nodes<br>3. Practical requirements: a good solution may be more useful than waiting a long time for the perfect solution <br><br>

### B4. Hand trace: Bartica to Ituni

Straight-line distances to Ituni (km) used for A*:

| Town | h (km) |
|---|---|
| Annai | 200.5 |
| Anna Regina | 193.9 |
| Bartica | 105.1 |
| Charity | 210.6 |
| Corriverton | 130.2 |
| Diamond | 131.6 |
| Georgetown | 141.8 |
| Ituni | 0.0 |
| Kurupukari | 106.7 |
| Kwakwani | 36.7 |
| Lethem | 294.4 |
| Linden | 53.5 |
| Mahaica | 133.1 |
| Mahdia | 102.6 |
| New Amsterdam | 113.8 |
| Ogle | 138.3 |
| Parika | 148.7 |
| Rosignol | 114.6 |
| Soesdyke | 112.5 |
| Timehri | 108.8 |
| Vreed en Hoop | 142.2 |


**BFS** (expansion order, fringe at each step):
<br><br>

**Expansion order:**

Bartica → Mahdia → Parika → Linden → Anna Regina → Vreed en Hoop → Ituni

**Fringe after each expansion:**

| Expanded node | g (km) | Fringe after expansion |
|---|---|---|
| Bartica | 0.0 | Mahdia (265.8), Parika (235.2) |
| Mahdia | 265.8 | Parika (235.2), Linden (461.3) |
| Parika | 235.2 | Linden (461.3), Anna Regina (293.3), Vreed en Hoop (266.1) |
| Linden | 461.3 | Anna Regina (293.3), Vreed en Hoop (266.1), Ituni (527.1), Kurupukari (688.1), Kwakwani (568.5), Soesdyke (536.6) |
| Anna Regina | 293.3 | Vreed en Hoop (266.1), Ituni (527.1), Kurupukari (688.1), Kwakwani (568.5), Soesdyke (536.6), Charity (318.5) |
| Vreed en Hoop | 266.1 | Ituni (527.1), Kurupukari (688.1), Kwakwani (568.5), Soesdyke (536.6), Charity (318.5), Georgetown (281.6) |
| Ituni | 527.1 | Goal reached |


**UCS** (expansion order, fringe and g at each step):
<br><br>

**Expansion order:**

Bartica → Parika → Mahdia → Vreed en Hoop → Georgetown → Ogle → Anna Regina → Diamond → Soesdyke → Charity → Mahaica → Timehri → Rosignol → Linden → New Amsterdam → Ituni

The fringe is ordered by increasing g(n).

| Expanded node | g (km) | Fringe after expansion |
|---|---|---|
| Bartica | 0.0 | Parika (235.2), Mahdia (265.8) |
| Parika | 235.2 | Mahdia (265.8), Vreed en Hoop (266.1), Anna Regina (293.3) |
| Mahdia | 265.8 | Vreed en Hoop (266.1), Anna Regina (293.3), Linden (461.3) |
| Vreed en Hoop | 266.1 | Georgetown (281.6), Anna Regina (293.3), Linden (461.3) |
| Georgetown | 281.6 | Ogle (288.6), Anna Regina (293.3), Diamond (294.6), Timehri (325.4), Linden (461.3) |
| Ogle | 288.6 | Anna Regina (293.3), Diamond (294.6), Mahaica (321.6), Timehri (325.4), Linden (461.3) |
| Anna Regina | 293.3 | Diamond (294.6), Charity (318.5), Mahaica (321.6), Timehri (325.4), Linden (461.3) |
| Diamond | 294.6 | Soesdyke (315.7), Charity (318.5), Mahaica (321.6), Timehri (325.4), Linden (461.3) |
| Soesdyke | 315.7 | Charity (318.5), Mahaica (321.6), Timehri (324.2), Linden (391.0) |
| Charity | 318.5 | Mahaica (321.6), Timehri (324.2), Linden (391.0) |
| Mahaica | 321.6 | Timehri (324.2), Rosignol (387.2), Linden (391.0) |
| Timehri | 324.2 | Rosignol (387.2), Linden (391.0) |
| Rosignol | 387.2 | Linden (391.0), New Amsterdam (399.7) |
| Linden | 391.0 | New Amsterdam (399.7), Ituni (456.8), Kwakwani (498.2), Kurupukari (617.8) |
| New Amsterdam | 399.7 | Ituni (456.8), Corriverton (473.9), Kwakwani (498.2), Kurupukari (617.8) |
| Ituni | 456.8 | Goal reached |

**A\*** (expansion order, fringe with g, h, f at each step):
<br><br>
**Expansion order:**

Bartica → Mahdia → Parika → Vreed en Hoop → Georgetown → Diamond → Ogle → Soesdyke → Timehri → Linden → Mahaica → Ituni

Each fringe entry is represented as:

Town(g, h, f)

The fringe is ordered by increasing f.

| Expanded node | Fringe after expansion |
|---|---|
| Bartica | Mahdia (265.8, 102.6, 368.4); Parika (235.2, 148.7, 383.9) |
| Mahdia | Parika (235.2, 148.7, 383.9); Linden (461.3, 53.5, 514.8) |
| Parika | Vreed en Hoop (266.1, 142.2, 408.3); Anna Regina (293.3, 193.9, 487.2); Linden (461.3, 53.5, 514.8) |
| Vreed en Hoop | Georgetown (281.6, 141.8, 423.4); Anna Regina (293.3, 193.9, 487.2); Linden (461.3, 53.5, 514.8) |
| Georgetown | Diamond (294.6, 131.6, 426.2); Ogle (288.6, 138.3, 426.9); Timehri (325.4, 108.8, 434.2); Anna Regina (293.3, 193.9, 487.2); Linden (461.3, 53.5, 514.8) |
| Diamond | Ogle (288.6, 138.3, 426.9); Soesdyke (315.7, 112.5, 428.2); Timehri (325.4, 108.8, 434.2); Anna Regina (293.3, 193.9, 487.2); Linden (461.3, 53.5, 514.8) |
| Ogle | Soesdyke (315.7, 112.5, 428.2); Timehri (325.4, 108.8, 434.2); Mahaica (321.6, 133.1, 454.7); Anna Regina (293.3, 193.9, 487.2); Linden (461.3, 53.5, 514.8) |
| Soesdyke | Timehri (324.2, 108.8, 433.0); Linden (391.0, 53.5, 444.5); Mahaica (321.6, 133.1, 454.7); Anna Regina (293.3, 193.9, 487.2) |
| Timehri | Linden (391.0, 53.5, 444.5); Mahaica (321.6, 133.1, 454.7); Anna Regina (293.3, 193.9, 487.2) |
| Linden | Mahaica (321.6, 133.1, 454.7); Ituni (456.8, 0.0, 456.8); Anna Regina (293.3, 193.9, 487.2); Kwakwani (498.2, 36.7, 534.9); Kurupukari (617.8, 106.7, 724.5) |
| Mahaica | Ituni (456.8, 0.0, 456.8); Anna Regina (293.3, 193.9, 487.2); Rosignol (387.2, 114.6, 501.8); Kwakwani (498.2, 36.7, 534.9); Kurupukari (617.8, 106.7, 724.5) |
| Ituni | Goal reached |


| Algorithm | Route | Cost (km) | Optimal? |
|---|---|---|---|
| BFS | Bartica → Mahdia → Linden → Ituni | 527.1 | No |
| UCS | Bartica → Parika → Vreed en Hoop → Georgetown → Diamond → Soesdyke → Linden → Ituni | 456.8 | Yes |
| A* | Bartica → Parika → Vreed en Hoop → Georgetown → Diamond → Soesdyke → Linden → Ituni | 456.8 | Yes |

Why A* expanded fewer (or not fewer) nodes than UCS:<br>
UCS only uses the accumulated path cost g(n) to decide which node to expand while A<sup>*</sup> uses both the cost and estimated remaining distance to the goal.
---

## Part C: Route Planning in Guyana

### Autograder output

Paste the final lines of `python autograder.py --no-graphics`:

```
```

### Heuristic for the "hours" cost mode

Explain the speed you divide by and why it guarantees admissibility:

### C3.1 Results table

| Start → Goal | Mode | Algorithm | Cost | Expanded | ms | Route |
|---|---|---|---|---|---|---|
| | | BFS | | | | |
| | | DFS | | | | |
| | | UCS | | | | |
| | | Greedy | | | | |
| | | A* | | | | |

### C3.2 Analysis

### C3.3 Formulation critique

---

## Part D: Search vs. LLMs

### D1. Transcripts

For each instance: model and version, exact prompt, full response.

#### Instance 1

#### Instance 2

#### Instance 3

#### Instance 4 (8-puzzle)

#### Instance 5 (8-puzzle)

### D2. Evaluation

| Instance | LLM answer valid? | LLM cost | Optimal cost (A*/BFS) | Hallucinations? |
|---|---|---|---|---|
| | | | | |

### D3. Reflection (200–300 words)

---

## Generative AI Log

List every use of generative AI for this homework, excluding the Part D experiments above.



| Tool | What I asked | How I used the answer |
|---|---|---|
| | | |
