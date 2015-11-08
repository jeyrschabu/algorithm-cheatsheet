Graph
==========

NOTES:
- Breadth First Search: O(m + n) where m is the number of edges and n the number of vertices

```
class Node {
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
```