---
title: "Dijkstra's algorithm "
description: "Dijkstra's algorithm is a graph-search algorithm used to find the shortest path from a single source vertex to all other vertices in a weighted, direc"
date: 2023-04-21T00:44:47.024Z
tags: ["algorithm"]
---
<style type="text/css">
    ol { list-style-type: upper-alpha; }
</style>

## Dijkstra's algorithm 

Dijkstra's algorithm is a graph-search algorithm used to find the shortest path from a single source vertex to all other vertices in a weighted, directed graph with non-negative edge weights. 

- The algorithm, named after its creator Edsger W. Dijkstra, is widely used in network routing, navigation systems, and other applications that require finding the shortest path between points.

### How it works!

Dijkstra's algorithm maintains a set of unvisited vertices, and it works by iteratively selecting the vertex with the smallest known distance from the source vertex, visiting it, and updating the distance estimates for its neighboring vertices. Here's a high-level description of the algorithm:

1 Initialize the distance estimates: Set the distance estimate for the source vertex to 0 and the distance estimates for all other vertices to infinity.

2 Create a set of unvisited vertices and include all vertices in the graph.

3 While there are still unvisited vertices:
	
   1. Choose the vertex with the smallest known distance estimate from the source vertex that hasn't been visited yet. Mark it as visited.
	
   2. For each neighbor of the current vertex, calculate the distance from the source vertex to the neighbor through the current vertex. If this distance is smaller than the current distance estimate for the neighbor, update the neighbor's distance estimate with the newly calculated distance.

4 Once all vertices have been visited, the shortest path from the source vertex to all other vertices in the graph is found.

### Time Complexity
Dijkstra's algorithm has a time complexity of O(|V|^2) in its basic form, where |V| is the number of vertices in the graph. However, using a priority queue data structure, the time complexity can be improved to O(|V| + |E| * log(|V|)), where |E| is the number of edges in the graph.

It is important to note that Dijkstra's algorithm assumes that the edge weights are non-negative, as it relies on the property that a shorter path will never be discovered after visiting a vertex. If the graph contains negative-weight edges, the algorithm may produce incorrect results, and an alternative algorithm like Bellman-Ford should be used instead.

## Explain to Child

Imagine you want to go from your home to your friend's house, and there are many different paths you can take. Some paths are shorter, and some are longer. 

Dijkstra's algorithm is like a set of instructions to help you find the shortest path to get to your friend's house quickly.

Let's say you have a treasure map that shows all the paths to your friend's house. On this map, each path has a number that tells you how long it takes to walk.

Here's how Dijkstra's algorithm works like a game:

1 Start at your home and write the number 0 on it because it takes 0 minutes to get to where you are now.

2 Look at all the paths going from your home to the nearby houses, and choose the one with the smallest number (the quickest path).

3 Move to the next house and look at all the paths going from this house. Choose the quickest path and add the number from the path you took before.

4 Keep doing this, moving from house to house and always choosing the quickest path.

5 When you reach your friend's house, you have found the shortest path!

By following Dijkstra's algorithm, you can find the fastest way to get to your friend's house, even if there are many different paths to choose from. Just remember, this game works best when all the paths have positive numbers, which means they take some time to walk. If some paths have negative numbers (meaning you can travel back in time), this game might not work, and you'll need to play a different one.

## Java Implementation

```java
import java.util.Arrays;

public class DijkstraAlgorithm {

    private static final int NO_PARENT = -1;

    public static void main(String[] args) {
        int[][] adjacencyMatrix = {
                { 0, 4, 0, 0, 0, 0, 0, 8, 0 },
                { 4, 0, 8, 0, 0, 0, 0, 11, 0 },
                { 0, 8, 0, 7, 0, 4, 0, 0, 2 },
                { 0, 0, 7, 0, 9, 14, 0, 0, 0 },
                { 0, 0, 0, 9, 0, 10, 0, 0, 0 },
                { 0, 0, 4, 14, 10, 0, 2, 0, 0 },
                { 0, 0, 0, 0, 0, 2, 0, 1, 6 },
                { 8, 11, 0, 0, 0, 0, 1, 0, 7 },
                { 0, 0, 2, 0, 0, 0, 6, 7, 0 }
        };

        int sourceVertex = 0;
        dijkstraShortestPath(adjacencyMatrix, sourceVertex);
    }

    private static void dijkstraShortestPath(int[][] adjacencyMatrix, int sourceVertex) {
        int nVertices = adjacencyMatrix[0].length;

        int[] shortestDistances = new int[nVertices];
        Arrays.fill(shortestDistances, Integer.MAX_VALUE);
        shortestDistances[sourceVertex] = 0;

        boolean[] visitedVertices = new boolean[nVertices];

        int[] parents = new int[nVertices];
        Arrays.fill(parents, NO_PARENT);

        for (int i = 0; i < nVertices - 1; ++i) {
            int nearestVertex = -1;
            int shortestDistance = Integer.MAX_VALUE;

            for (int vertexIndex = 0; vertexIndex < nVertices; ++vertexIndex) {
                if (!visitedVertices[vertexIndex] && shortestDistances[vertexIndex] < shortestDistance) {
                    nearestVertex = vertexIndex;
                    shortestDistance = shortestDistances[vertexIndex];
                }
            }

            visitedVertices[nearestVertex] = true;

            for (int vertexIndex = 0; vertexIndex < nVertices; ++vertexIndex) {
                int edgeDistance = adjacencyMatrix[nearestVertex][vertexIndex];
                
                if (edgeDistance > 0 && ((shortestDistance + edgeDistance) < shortestDistances[vertexIndex])) {
                    parents[vertexIndex] = nearestVertex;
                    shortestDistances[vertexIndex] = shortestDistance + edgeDistance;
                }
            }
        }

        printSolution(sourceVertex, shortestDistances, parents);
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
The printSolution method prints the shortest path distances from the source vertex to all other vertices, as well as the actual paths. The printPath method is a helper function that recursively prints the path from the source vertex to a given vertex.

### Result
```
Vertex   Distance       Path
0 -> 1           4               0 1 
0 -> 2           12              0 1 2 
0 -> 3           19              0 1 2 3 
0 -> 4           21              0 7 6 5 4 
0 -> 5           11              0 7 6 5 
0 -> 6           9               0 7 6 
0 -> 7           8               0 7 
0 -> 8           14              0 1 2 8 
```

## Dijkstra vs Bellman-Ford

Dijkstra's algorithm and the Bellman-Ford algorithm are both like games that help you find the quickest way to get from one place to another on a map, where the map shows paths between different places (called points or vertices) and the time it takes to walk along those paths.

Dijkstra's game works best when all the paths have positive numbers, which means they take some time to walk. If some paths have negative numbers (which is like traveling back in time), Dijkstra's game might not work. But, Dijkstra's game can help you find the quickest path very fast!

Bellman-Ford's game is a bit different. It can still help you find the quickest way even if some paths have negative numbers. 
But, it can also tell you if it's impossible to find the quickest way because the paths keep going in circles with negative numbers, making you go back in time. 
This game is a bit slower than Dijkstra's game but works in more situations.

In short, both games help you find the quickest way to get somewhere on a map, but they have different rules and work better in different situations. 

Dijkstra's game is faster but only works when all paths have positive numbers, while Bellman-Ford's game works even if some paths have negative numbers but is a bit slower.


## Source
GPT-4
