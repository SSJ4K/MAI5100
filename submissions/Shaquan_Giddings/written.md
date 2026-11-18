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

1.
2.
3.
4.

### B3. Proofs about heuristics

1.
2.
3.

### B4. Hand trace: Bartica to Ituni

Straight-line distances to Ituni (km) used for A*:

| Town | h (km) |
|---|---|
| | |

**BFS** (expansion order, fringe at each step):

**UCS** (expansion order, fringe and g at each step):

**A\*** (expansion order, fringe with g, h, f at each step):

| Algorithm | Route | Cost (km) | Optimal? |
|---|---|---|---|
| BFS | | | |
| UCS | | | |
| A* | | | |

Why A* expanded fewer (or not fewer) nodes than UCS:

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
