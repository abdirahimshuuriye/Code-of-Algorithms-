# Code-of-Algorithms-

# ================================================
# Traveling Salesman Problem (Brute Force)
# ================================================
from itertools import permutations

def tsp_brute_force(graph, start=0):
    print("---- TSP Brute Force ----")
    n = len(graph)
    vertices = list(range(n))
    vertices.remove(start)
    min_path = float('inf')
    best_route = []

    for perm in permutations(vertices):
        current_path = [start] + list(perm) + [start]
        current_cost = sum(graph[current_path[i]][current_path[i+1]] for i in range(n))
        if current_cost < min_path:
            min_path = current_cost
            best_route = current_path

    print("Best route:", best_route)
    print("Minimum cost:", min_path)
    print()

# Example graph (4 cities)
graph = [
    [0, 10, 15, 20],
    [10, 0, 35, 25],
    [15, 35, 0, 30],
    [20, 25, 30, 0]
]
tsp_brute_force(graph)

# ================================================
# Set Cover Problem (Greedy)
# ================================================
def greedy_set_cover(universe, subsets):
    print("---- Set Cover Greedy ----")
    elements = set(universe)
    cover = []
    while elements:
        subset = max(subsets, key=lambda s: len(s & elements))
        cover.append(subset)
        elements -= subset
    for i, s in enumerate(cover):
        print(f"Set {i+1}: {s}")
    print()

# Example
U = {1, 2, 3, 4, 5}
S = [{1, 2}, {2, 3, 4}, {4, 5}]
greedy_set_cover(U, S)

# ================================================
# Vertex Cover Problem (Greedy Approximation)
# ================================================
def greedy_vertex_cover(edges):
    print("---- Vertex Cover Greedy ----")
    cover = set()
    while edges:
        degree = {}
        for u, v in edges:
            degree[u] = degree.get(u, 0) + 1
            degree[v] = degree.get(v, 0) + 1
        u = max(degree, key=degree.get)
        cover.add(u)
        edges = [(a, b) for a, b in edges if a != u and b != u]
    print("Vertex Cover:", cover)

# Example
edges = [('A', 'B'), ('A', 'C'), ('B', 'C'), ('C', 'D')]
greedy_vertex_cover(edges)
