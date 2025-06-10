# Problem 1
 Algorithm Overview
A resistor network can be represented as a graph, where:

Nodes represent connection points (junctions),

Edges represent resistors, with resistance as the edge weight.

To compute the equivalent resistance, the algorithm must:

Detect series connections and collapse them.

Detect parallel connections and reduce them.

Repeat until a single edge connects the two terminals.

 Core Logic Description
Series Rule: If a node connects exactly two resistors, and it’s not a terminal, these are in series:
𝑅
𝑒
𝑞
=
𝑅
1
+
𝑅
2
R 
eq
​
 =R 
1
​
 +R 
2
​
 

Parallel Rule: If multiple resistors connect the same pair of nodes, they are in parallel:
1
𝑅
𝑒
𝑞
=
1
𝑅
1
+
1
𝑅
2
+
…
R 
eq
​
 
1
​
 = 
R 
1
​
 
1
​
 + 
R 
2
​
 
1
​
 +…

The algorithm uses graph simplification, repeatedly replacing such combinations with equivalent resistors.

 Python Implementation with NetworkX
python
Kopyala
Düzenle
import networkx as nx

def simplify_resistor_graph(G, terminal_a, terminal_b):
    while True:
        changed = False

        # Step 1: Parallel reduction
        for u, v in list(G.edges()):
            edges = list(G.get_edge_data(u, v).values())
            if len(edges) > 1:
                # Reduce parallel resistors
                total_reciprocal = sum(1.0 / edge['resistance'] for edge in edges)
                R_eq = 1.0 / total_reciprocal
                # Remove all and add one equivalent
                G.remove_edges_from([(u, v)] * len(edges))
                G.add_edge(u, v, resistance=R_eq)
                changed = True

        # Step 2: Series reduction
        for node in list(G.nodes()):
            if node in (terminal_a, terminal_b):
                continue
            neighbors = list(G[node])
            if len(neighbors) == 2:
                u, v = neighbors
                if G.number_of_edges(node, u) == 1 and G.number_of_edges(node, v) == 1:
                    R1 = G.edges[node, u]['resistance']
                    R2 = G.edges[node, v]['resistance']
                    R_eq = R1 + R2
                    G.remove_node(node)
                    G.add_edge(u, v, resistance=R_eq)
                    changed = True
                    break  # Re-scan graph after change

        if not changed:
            break

    # Final resistance
    if G.has_edge(terminal_a, terminal_b):
        return G.edges[terminal_a, terminal_b]['resistance']
    else:
        return float('inf')  # No path

# Example 1: Simple series
G1 = nx.MultiGraph()
G1.add_edge('A', 'B', resistance=5)
G1.add_edge('B', 'C', resistance=10)
print("Series Resistance:", simplify_resistor_graph(G1, 'A', 'C'))  # 15Ω

# Example 2: Parallel
G2 = nx.MultiGraph()
G2.add_edge('A', 'B', resistance=10)
G2.add_edge('A', 'B', resistance=20)
print("Parallel Resistance:", simplify_resistor_graph(G2, 'A', 'B'))  # 6.67Ω

# Example 3: Nested
G3 = nx.MultiGraph()
G3.add_edge('A', 'B', resistance=10)
G3.add_edge('B', 'C', resistance=10)
G3.add_edge('C', 'D', resistance=10)
G3.add_edge('A', 'D', resistance=5)
print("Nested Resistance:", simplify_resistor_graph(G3, 'A', 'D'))  # Complex reduction
 Description of Handling for 3 Example Configurations
Simple Series (A-B-C)
Reduces via linear chain: 10Ω + 5Ω = 15Ω

Simple Parallel (A-B with two paths)
Reduces using:
1
𝑅
=
1
10
+
1
20
⇒
𝑅
=
6.67
 
Ω
R
1
​
 = 
10
1
​
 + 
20
1
​
 ⇒R=6.67 Ω

Nested (with a shortcut)
Handles both parallel and series:
Reduces B-C-D as 20Ω, then computes parallel of A-D (5Ω) and A-B-C-D (30Ω)
Final 
𝑅
=
(
1
5
+
1
30
)
−
1
≈
4.29
 
Ω
R=( 
5
1
​
 + 
30
1
​
 ) 
−1
 ≈4.29 Ω

 Complexity & Efficiency
Best case: 
𝑂
(
𝑛
)
O(n) when nodes are reducible in few steps

Worst case: 
𝑂
(
𝑛
2
)
O(n 
2
 ) due to re-traversing for each simplification

Improvements:

Use a union-find structure to speed up parallel detection

Apply memoization or caching for known substructures

Use DFS with tagging to handle loops systematically


