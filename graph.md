###Graph
==========

NOTES:
- Breadth First Search: O(m + n) where m is the number of edges and n the number of vertices
- Depth First Search

```java
class Node { //using adjacency list
    int data;
    boolean visited;
    List<Node> list = new ArrayList<>();
    void print() {};
}

void bfs(Node root) {
    Queue<Integer> queue = new LinkedList<>();
    queue.add(root);
    root.visited = true;
    while (!queue.isEmpty()) {
        Node current = queue.poll();
        current.print();
        for (Node i : current.list) {
            if (!i.visited) {
                current.visited = true;
                queue.add(current);
            }
        }
    }
}

int connectedComponents(List<Node> nodes) {
    int count = 0;

    for (Node n : nodes) {
        n.visited = false;
    }

    for (Node n : nodes) {
        if (!n.visited) {
            count++;
            bfs(n);
        }
    }

    return count;
}

void dfs(Node start) {
    if (start == null) {
        return;
    }

    start.visited = true;
    for (Node a : start.list) {
        if (!a.visited) {
            dfs(a);
        }
    }   
}

boolean isReachable(List<Node> nodes, Node source, Node target) {
    List<Node> queue = new LinkedList<>();
    for (Node n : nodes) {
        n.visited = false;
    }

    source.visited = true;
    queue.add(source);
    while (!queue.isEmpty()) {
        Node current = queue.poll();
        for (Node n : current.list) {
            if (!n.visited && n.equals(target)) {
                return true;
            }

            n.visited = true;
            queue.add(n);
        }
    }

    return false;
}
```

###DAGs

```java
enum Color {
    GRAY,
    BLACK
}

void topSort(List<Node> nodes) {
    List<Node> sorted = new ArrayList<>();
    Map<Node, Color> state = new HashMap<>();
    Set<Node> path = new LinkedHashSet<>();
    List<Set<Node>> paths = new ArrayList<>();
    for (Node n : nodes) {
        outOrder.put(n, 0);
    }

    for (Node n : nodes) {
        dfs(n, sorted, state, path, paths, outOrder);
    }
}

void dfs(Node node, 
         List<Node> sorted, 
         Map<Node, Color> state, 
         Set<Node> path,
         List<Set<Node>> paths,
         Map<String, Integer> outOrder) {

    state.put(node, Color.GRAY);
    path.add(node);

    for (Node n : node.list) {
        Color color = state.get(n);
        if (color == GRAY) throw new IllegalStateException("Cycle Detection");
        if (color == BLACK) continue;
        path.add(n);
        Set<Node> newPath = new LinkedHashSet<>(path);
        dfs(n, sorted, state, new LinkedHashSet(newPath));
    }

    state.put(node, Color.BLACK);
    sorted.add(node);
    paths.add(path);

    for (Node n : node.list) {
        outOrder(n, outOrder.get(n) + 1);
    }
}
```

###Single Source Shortest Path

```java
void dijkstra(int graph[][], int source) {
    int distance[] = new int[TOTAL];
    Boolean shortestPaths[] = new Boolean[TOTAL];
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
    for (int i = 0; i < TOTAL; i++) {
        System.out.println(distance[i]);
    }
}

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