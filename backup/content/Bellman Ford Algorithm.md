---
title: "Bellman Ford Algorithm"
description: "Imagine you want to visit your friend's house, but there are many paths to get there. You want to find the quickest way, so you don't spend too much t"
date: 2023-04-21T00:38:19.943Z
tags: ["algorithm"]
---
## Bellman Ford Algorithm
The Bellman-Ford algorithm is a graph-search algorithm 

- It is used to find the shortest path from a single source vertex to all other vertices in a weighted, directed graph. 
- The algorithm can handle graphs with negative-weight edges but will detect if there is a negative-weight cycle, which means that no shortest path exists.

The Bellman-Ford algorithm works by iteratively updating distance estimates (weights) for each vertex in the graph until the shortest path from the source vertex to each of the other vertices is found. Here's a high-level description of the algorithm:

1 Initialize the distance estimates: Set the distance estimate for the source vertex to 0 and the distance estimates for all other vertices to infinity.

2 Relax the edges: For each vertex in the graph, go through its edges (u, v) with weight w(u, v) and perform the following:
	a. If the distance estimate from the source vertex to vertex v is greater than the distance estimate from the source vertex to vertex u plus the weight of the edge w(u, v), update the distance estimate for vertex v to be the sum of the distance estimate for vertex u and the edge weight w(u, v).

3 Repeat step 2 (relaxing the edges) |V| - 1 times, where |V| is the number of vertices in the graph. After |V| - 1 iterations, the shortest path to each vertex should be found.

4 Check for negative-weight cycles: Go through each edge (u, v) with weight w(u, v) again. If the distance estimate from the source vertex to vertex v is still greater than the distance estimate from the source vertex to vertex u plus the weight of the edge w(u, v), there must be a negative-weight cycle in the graph, and the algorithm cannot find a valid shortest path.

The Bellman-Ford algorithm has a time complexity of O(|V| * |E|), where |V| is the number of vertices and |E| is the number of edges in the graph. This makes it slower than other shortest-path algorithms like Dijkstra's, but it has the advantage of being able to handle graphs with negative-weight edges.

## Explain to a child
Imagine you want to visit your friend's house, but there are many paths to get there. You want to find the quickest way, so you don't spend too much time walking. 

The Bellman-Ford algorithm is like a set of instructions that helps you find the shortest route.

Let's say you have a map with all the possible paths, and each path has a number that tells you how long it takes to walk. The Bellman-Ford algorithm works like this:

1 You start at your house and mark it with the number 0 because it takes 0 minutes to get to where you are now.

2 Then, you look at all the paths from your house to the nearby houses and choose the one with the smallest number (the quickest path).

3 Next, you move to the next house and repeat the process. You look at all the paths from this house and choose the quickest path, but you also add the number from the path you took before.

4 You keep doing this until you reach your friend's house, always choosing the path with the smallest total number.

Sometimes you might find a faster path after you've already visited a house. In that case, you can update the numbers and take the new faster path instead.

By following the Bellman-Ford algorithm, you'll be able to find the quickest way to your friend's house, even if there are many paths to choose from.

## Java Implementation

```java
public class BellmanFordAlgorithmOptimized {

    private static final int INFINITY = Integer.MAX_VALUE;
    private static final int NO_PARENT = -1;

    public static void main(String[] args) {
        int[][] graph = {
                { 0, -1, 4, 0, 0 },
                { 0, 0, 3, 2, 2 },
                { 0, 0, 0, 0, 0 },
                { 0, 1, 5, 0, 0 },
                { 0, 0, 0, -3, 0 }
        };

        int sourceVertex = 0;
        bellmanFord(graph, sourceVertex);
    }

    private static void bellmanFord(int[][] graph, int sourceVertex) {
        int nVertices = graph.length;
        int[] distances = new int[nVertices];
        int[] parents = new int[nVertices];

        for (int i = 0; i < nVertices; ++i) {
            distances[i] = INFINITY;
            parents[i] = NO_PARENT;
        }

        distances[sourceVertex] = 0;

        boolean updated;
        for (int i = 1; i < nVertices; ++i) {
            updated = false;
            for (int vertex = 0; vertex < nVertices; ++vertex) {
                for (int neighbor = 0; neighbor < nVertices; ++neighbor) {
                    int edgeWeight = graph[vertex][neighbor];
                    if (edgeWeight != 0 && distances[vertex] != INFINITY && distances[vertex] + edgeWeight < distances[neighbor]) {
                        distances[neighbor] = distances[vertex] + edgeWeight;
                        parents[neighbor] = vertex;
                        updated = true;
                    }
                }
            }
            if (!updated) {
                break;
            }
        }

        for (int vertex = 0; vertex < nVertices; ++vertex) {
            for (int neighbor = 0; neighbor < nVertices; ++neighbor) {
                int edgeWeight = graph[vertex][neighbor];
                if (edgeWeight != 0 && distances[vertex] != INFINITY && distances[vertex] + edgeWeight < distances[neighbor]) {
                    System.out.println("Graph contains a negative-weight cycle");
                    return;
                }
            }
        }

        printSolution(sourceVertex, distances, parents);
    }

    private static void printSolution(int startVertex, int[] distances, int[] parents) {
        int nVertices = distances.length;
        System.out.print("Vertex\t Distance\tPath");

        for (int vertexIndex = 0; vertexIndex < nVertices; vertexIndex++) {
            if (vertexIndex != startVertex) {
                System.out.print("\n" + startVertex + " -> ");
                System.out.print(vertexIndex + " \t\t ");
                System.out.print(distances[vertexIndex] + "\t\t ");
                printPath(vertexIndex, parents);
                System.out.print("\n");
            }
        }
    }

    private static void printPath(int currentVertex, int[] parents) {
        if (currentVertex == NO_PARENT) {
            return;
        }
        printPath(parents[currentVertex], parents);
        System.out.print(currentVertex + " ");
    }
}
```
This Java implementation of the Bellman-Ford algorithm finds the shortest paths from a single source vertex to all other vertices in a graph represented by an adjacency matrix. It also checks for negative-weight cycles and reports if one is found. The printSolution and printPath methods print the shortest path distances from the source vertex to all other vertices, as well as the actual paths.

The optimized implementation has a boolean variable updated which is set to true only if an update happens during the relaxation step. If no updates are made in a complete iteration through all edges, the algorithm terminates

### Result
```
Vertex   Distance       Path
0 -> 1           -1              0 1 

0 -> 2           2               0 1 2 

0 -> 3           -2              0 1 4 3 

0 -> 4           1               0 1 4 


```

## Source 
GPT-4
