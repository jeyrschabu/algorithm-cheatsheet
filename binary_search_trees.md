Binary Search Tree
==========

NOTES:
- BST property is such that a node's left subtree value is always at most its value
- Node x, left(x) =< x. Also right(x) > x

Implementations:



```
class Node<V> {
    Node parent;
    Node left;
    Node right;
    V value;
    Node(Node parent, Node left, Node right, V value) {
        this.parent = parent;
        this.left = left;
        this.right = right;
        this.value = value;
    }
}
```

[INORDER TREE WALK]

![alt text](assets/InOrderTraversalBinaryTree.jpg "Inorder traversal")
```
void inorder(Node node) {
    if (node != null) {
        inorder(node.left);
        System.out.println(node);
        inorder(node.right);
    }
}
```
[\INORDER TREE WALK]

