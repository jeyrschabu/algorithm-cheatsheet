Graph
==========

NOTES:
- Breadth First Search: O(m + n) where m is the number of edges and n the number of vertices
- Depth First Search

```
class Node { //using adjacency list
    int data;
    boolean visited;
    List<Node> items;
    void print() {}
}
void bfs(Node root) {
    List<Integer> queue = new LinkedList<>();
    root.visited = true;
    queue.add(root);
    Node current;
    while (!queue.isEmpty()) {
        current = queue.poll();
        current.print();
        for (Node i in current.list) {
            if (!i.visited) {
                current.visited = true;
                queue.add(current);
            }
        }
    }
}
void dfs(Node start) {
    Stack<Node> stack = new Stack<Node>();
    start.visited = true
    stack.push(start);
    while (!stack.isEmpty()) {
        Node p = stack.pop();
        for (Node a : p.list) {
            if (!a.visited) {
                stack.push(a);
                dfs(a);
            }
        }
    }
}
```
- Single Source Shortest Path

[DIJKSTRA]
```
void dijkstra(int graph[][], int source) {
    int distance[] = new int[TOTAL];
    Boolean shortestPaths = new Boolean[TOTAL];
    for (int i = 0; i < TOTAL; i++) {
        distance[i] = Integer.MAX_VALUE;
        shortestPaths[i] = false;
    }
    distance[source] = 0;
    for (int i = 0; i < TOTAL; i++) {
        int current = minDistance(distance, shortestPaths);
        shortestPaths[current] = true;
        for (int j = 0; j < TOTAL; j++) {
            if (shortestPaths[j] && graph[i][j] != 0
                && distance[j] != Integer.MAX_VALUE
                && distance[j] + graph[i][j] < distance[j]) distance[j] = distance[i] + graph[i][j];
        }
    }
    //print the distance from source
    for (int i = 0; i < TOTAL; i++) S.O.P(distance[i]);
}
```
[/DIJKSTRA]

[BELLMANFORD]
```
Integer [][] bellmanFord(Integer[][] weight, int source) throws Exception {
    final int SIZE = weight.length;
    final int EVE = -1;//to indicate no predecessor
    final int INFINITY = Integer.MAX_VALUE;
    //initialize
    Integer[] pred = new Integer[SIZE];
    Integer[] minDist = new Integer[SIZE];
    Arrays.fill(pred, EVE);
    Arrays.fill(minDist, INFINITY);
    //set minDist[source] = 0 because source is 0 distance from itself.
    minDist[source] = 0;
    //relax the edge set V-1 times to find all shortest paths
    for (int i = 1; i < minDist.length - 1; i++) {
      for (int v = 0; v < SIZE; v++) {
        for (int x : adjacency(weight, v)) {
          if (minDist[x] > minDist[v] + weight[v][x]) {
            minDist[x] = minDist[v] + weight[v][x];
            pred[x] = v;
          }
        }
      }
    }
    //detect cycles if any
    for (int v = 0; v < SIZE; v++) {
      for (int x : adjacency(weight, v)) {
        if (minDist[x] > minDist[v] + weight[v][x]) {
          throw new Exception("Negative cycle found");
        }
      }
    }
    Integer[][] result = {pred, minDist};
    return result;
  }
  List<Integer> adjacency(Integer[][] graph, int v) {
    List<Integer> result = new ArrayList<Integer>();
    for (int x = 0; x < graph.length; x++) {
      if (graph[v][x] != null) {
        result.add(x);
      }
    }
    return result;
  }
```
[/BELLMANFORD]