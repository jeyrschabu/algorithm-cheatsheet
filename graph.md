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
void dfs(Node root) {
    root.visited = true;
    for (Node i in root.items) {
        if (!i.visited) {
            dfs(i);
        }
    }
}
```

[SHORTESTPATH]
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
[/SHORTESTPATH]