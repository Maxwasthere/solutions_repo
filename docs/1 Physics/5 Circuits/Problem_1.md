# Circuits

## Introduction

Calculating the equivalent resistance in electrical circuits is a fundamental task in both theoretical and applied physics. Traditionally, this is done by successively applying series and parallel resistance rules. However, as circuits become more complex—with nested configurations, multiple loops, and redundant paths—this method becomes inefficient and error-prone.

Graph theory offers a structured and algorithmic alternative to this problem:

- A **circuit** can be modeled as an **undirected weighted graph**, where:

    - **Nodes** represent electrical junctions.

    - **Edges** represent resistors with **weights** corresponding to their resistance values.


- This abstraction enables the use of well-established graph algorithms to:

    - Identify series and parallel connections.

    - Simplify the network step-by-step.

    - Automate the calculation of the total or **equivalent resistance** between any two terminal nodes.

This approach is particularly valuable for:

- Complex circuits involving multiple loops and nested structures.

- Automated analysis and simulation.

- Deepening understanding of the connection between electrical systems and graph-theoretical models.

## Algorithm Description

To compute the equivalent resistance between two points in an electrical circuit, we can model the circuit as a **weighted undirected graph**, where:

- **Nodes** represent electrical junctions (connection points).

- **Edges** represent resistors, each assigned a weight equal to its resistance value.

This representation allows us to apply **graph-based algorithms** to simplify the circuit by systematically identifying and reducing **series** and **parallel** resistor groups.

### Description of the Algorithm:

1. **Graph Construction**:  
   The circuit is first translated into a graph. Each junction in the circuit becomes a node, and each resistor becomes an edge between two nodes, labeled with its resistance.

2. **Detection of Series Combinations**:  
   A **series** configuration is detected when a node connects **exactly two resistors** and is not a terminal node (i.e., not the start or end of the network). The resistors connected through this intermediate node are then collapsed into a single resistor:  
   $R_{eq} = R_1 + R_2$

3. **Detection of Parallel Combinations**:  
   A **parallel** configuration exists when **two or more resistors** connect the **same pair of nodes**. These are replaced with a single equivalent resistor using the formula:  
   $\frac{1}{R_{eq}} = \frac{1}{R_1} + \frac{1}{R_2} + \dots + \frac{1}{R_n}$

4. **Graph Simplification**:  
   After identifying series or parallel combinations, the corresponding nodes and edges are removed or updated, and a new edge representing the equivalent resistance is added in their place.

5. **Repeat Until Reduced**:  
   Steps 2–4 are repeated in a loop until the graph contains only two nodes (the source and destination) connected by a single equivalent edge.

6. **Return Final Resistance**:  
   The resistance value of the final edge is the total equivalent resistance of the circuit between the selected terminals.

### Practical Considerations:

- The algorithm needs to **avoid collapsing** terminal nodes (such as the power source and ground).

- **Nested combinations** (e.g., series of parallel groups, or parallel of series groups) are automatically handled by the repetition of the simplification loop.

- The algorithm assumes all resistors are **linear and passive** (i.e., they obey Ohm’s Law and have no directionality or power source themselves).


## Pseudocode – Identifying Series and Parallel Connections

### Pseudocode:

#### Function: Identify and Simplify Series Connections

```
function simplify_series(G, start, end):
simplified = false

for each node v in G:
    if v ≠ start and v ≠ end and degree(v) == 2:
        neighbors = get_neighbors(v)
        u = neighbors[0]
        w = neighbors[1]

        if exactly one edge between (v, u) and one edge between (v, w):
            R1 = resistance of edge (v, u)
            R2 = resistance of edge (v, w)
            R_eq = R1 + R2

            remove edges (v, u) and (v, w)
            remove node v
            add edge (u, w) with resistance R_eq

            simplified = true

return simplified

```
#### Function: Identify and Simplify Parallel Connections

```
function simplify_parallel(G):
simplified = false
for each pair of nodes (u, v) in G:
    edges = get_all_edges_between(u, v)

    if length(edges) > 1:
        resistances = [resistance of each edge in edges]
        R_eq = 1 / sum(1 / R for R in resistances)

        remove all edges between u and v
        add one edge (u, v) with resistance R_eq

        simplified = true

return simplified
```

---

### Explanation of the Pseudocode:

#### 1. **Series Detection Logic**

- The function `simplify_series` iterates over all nodes in the graph.

- It **skips terminal nodes** (start and end) to avoid breaking the main circuit path.


- For each internal node $v$:

  - It checks if the degree of $v$ is 2 (i.e., connected to exactly two neighbors).
  - It confirms that there's only **one edge** to each neighbor — a requirement for a **pure series** connection.
  - It calculates the **equivalent resistance** as $R_{eq} = R_1 + R_2$.
  - It removes the intermediate node and the two old resistors, and replaces them with a new resistor between the neighbors.

#### 2. **Parallel Detection Logic**

- The function `simplify_parallel` examines every pair of nodes $(u, v)$.

- If there are **multiple edges** (i.e., multiple resistors) between the same pair of nodes, they are in **parallel**.

- It gathers all resistance values and computes the equivalent using:  
  $\frac{1}{R_{eq}} = \frac{1}{R_1} + \frac{1}{R_2} + \dots$

- It removes all old edges and replaces them with a single edge with resistance $R_{eq}$.

#### 3. **Output Behavior**

- Both functions return a boolean `simplified` to indicate whether any simplification occurred during that pass.

- This allows the main loop to **repeat the simplification** as long as the graph keeps changing.

---


These two pseudocode functions are the **core mechanisms** that allow the algorithm to detect and simplify both basic and **nested** resistor configurations. By embedding them into an iterative loop, the algorithm naturally breaks down complex circuits into simpler ones:

- First, it collapses any visible series or parallel groups.

- Then, simplification may **expose deeper combinations** that weren’t initially detectable.

- Eventually, the circuit graph reduces to a single equivalent resistor between the input and output terminals — even if the original structure included **multi-level nested groups**.

## Pseudocode – Iterative Graph Reduction Until Single Equivalent Resistance

This pseudocode describes the full loop that continuously applies simplification rules until the circuit reduces to a single equivalent resistance between two terminal nodes.

### Pseudocode:

```
function compute_equivalent_resistance(G, start, end):

while true:
simplified_series = simplify_series(G, start, end)
simplified_parallel = simplify_parallel(G)

    if not simplified_series and not simplified_parallel:
        break

if edge exists directly between start and end:
    return resistance of that edge
else:
    return "Circuit is not fully connected or reducible"
```

### Explanation of the Algorithm:

1. **Loop Structure**:  

   The algorithm enters a loop where it repeatedly applies two simplification functions:
   - `simplify_series()`: Detects and merges series-connected resistors.
   - `simplify_parallel()`: Detects and merges parallel-connected resistors.


2. **Termination Condition**:  

   The loop exits when **no changes** are made during a complete pass — meaning the graph cannot be simplified further.

3. **Final Result**:  

   After exiting the loop, the algorithm checks whether a **single edge** remains between the terminal nodes:
   
   - If yes: the edge's resistance is returned as the **equivalent resistance**.
   - If not: the circuit is either **not fully connected** or contains configurations not handled by the algorithm.

4. **Recursive Simplicity through Iteration**:  

   Even **nested combinations** (such as a parallel group containing series resistors) are simplified without additional logic — because inner structures are eventually exposed as the graph becomes simpler with each pass.

5. **Modular Design**:  

   The algorithm is modular: simplification logic is abstracted into separate functions (`simplify_series` and `simplify_parallel`) and the core loop just controls **when to stop**.

This design ensures correctness, scalability, and clarity for complex circuits.

## Handling Nested Combinations

Nested combinations occur when series and parallel resistor configurations are layered within each other — for example:

- A **series path** that contains a **parallel sub-group**  
- A **parallel structure** in which one or more branches are themselves made of **series resistors**  
- Multiple layers of alternating series and parallel combinations

### How the Algorithm Handles Nested Combinations:

The key to handling nested configurations lies in the algorithm's **iterative simplification approach**, not in explicitly detecting nesting.

#### 1. **Iterative Reduction Unfolds the Nesting Naturally**:

- The algorithm does **not attempt to identify the entire nested structure in one pass**.

- Instead, it **simplifies whatever it can detect** in each iteration (series or parallel groups).

- As these outer layers are simplified, the **inner nested structures are gradually exposed**.

- On the next pass, previously "hidden" configurations become reducible.

#### 2. **Example**:

Imagine a circuit with the following configuration:

- $R_1$ and $R_2$ in series  
- This combination is in parallel with $R_3$  
- That result is in series with $R_4$

Although this is a nested structure, the algorithm handles it as:

- **First Pass**: Combines $R_1 + R_2$ into one resistor ($R_{12}$)  
- **Second Pass**: Detects and simplifies $R_{12} \parallel R_3$  
- **Third Pass**: Adds the result in series with $R_4$

No special logic is needed for nesting — it resolves **automatically** over multiple iterations.

#### 3. **Why This Works**:

- Series and parallel rules apply **locally**.  
- Each simplification **reduces the graph** and **simplifies the topology**.  
- Eventually, **only the start and end nodes remain**, connected by a single equivalent resistor.

### Summary:

Instead of trying to break down the entire nested structure at once, the algorithm keeps things simple: it just looks for the basic series and parallel combinations it can reduce right now. Once those are simplified, new combinations start to show up naturally. By repeating this process, the more complex, nested parts of the circuit are handled step by step — no need for special rules or deep inspection. In the end, everything gets reduced to a single resistance between the two terminal nodes.
