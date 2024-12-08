https://leetcode.com/problems/course-schedule-ii/

## Topological Sorting: A Comprehensive Guide

Topological sorting is a graph algorithm used to linearly order the vertices of a directed acyclic graph (DAG) such that for every directed edge `u -> v`, vertex `u` comes before `v` in the ordering.

### Method 1: Depth-First Search (DFS) with Cycle Detection

**Algorithm:**

1. **Initialization:**
   * Create a visited set to track visited nodes.
   * Create a current_path set to detect cycles.
   * Create a stack to store the topological order.

2. **DFS Traversal:**
   - For each unvisited node:
     - Mark the node as visited and add it to the current_path set.
     - Recursively visit all its neighbors.
     - If a neighbor is already in the current_path set, a cycle is detected.
     - After processing all neighbors, remove the node from the current_path set and push it onto the stack.

3. **Topological Order:**
   - Reverse the stack to obtain the topological order.

**Python Implementation:**

```python
from collections import defaultdict

def topological_sort(graph):
    visited = set()
    stack = []
    current_path = set()

    def dfs_visit(node):
        nonlocal cycle
        if node in current_path:
            cycle = True
            return
        if node in visited:
            return
        visited.add(node)
        current_path.add(node)
        for neighbor in graph[node]:
            dfs_visit(neighbor)
        current_path.remove(node)
        stack.append(node)

    cycle = False
    for node in graph:
        dfs_visit(node)

    return stack[::-1] if not cycle else []
```

**Example:**

Consider the following graph:

```
A -> B -> C -> D
^      |
|      |
E -----+
```

The topological sort would be: `[E, A, B, C, D]`

### Method 2: Breadth-First Search (BFS) with Indegree

**Algorithm:**

1. **Initialization:**
   - Create a graph and calculate the indegree of each node.
   - Create a queue to store nodes with zero indegree.

2. **Topological Sort:**
   - While the queue is not empty:
     - Dequeue a node.
     - Add the node to the topological order.
     - Decrement the indegree of its neighbors.
     - If a neighbor's indegree becomes zero, enqueue it.

3. **Cycle Detection:**
   - If the final topological order doesn't contain all nodes, it indicates a cycle in the graph.

**Python Implementation:**

```python
from collections import defaultdict, deque

def topological_sort(numCourses, prerequisites):
    graph = defaultdict(list)
    indegree = [0] * numCourses

    for course, prerequisite in prerequisites:
        graph[prerequisite].append(course)
        indegree[course] += 1

    queue = deque([course for course in range(numCourses) if indegree[course] == 0])
    topological_order = []

    while queue:
        course = queue.popleft()
        topological_order.append(course)
        for neighbor in graph[course]:
            indegree[neighbor] -= 1
            if indegree[neighbor] == 0:
                queue.append(neighbor)

    return topological_order if len(topological_order) == numCourses else []
```

**Example:**

For the same graph as above, both methods would produce the same topological order: `[E, A, B, C, D]`.

**Choosing the Right Method:**

* **DFS:** More intuitive for understanding the topological ordering process, especially for smaller graphs.
* **BFS with Indegree:** Often more efficient, especially for large graphs with many nodes and edges.

The choice of algorithm depends on specific use cases and optimization considerations.
