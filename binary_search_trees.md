Binary Search Tree
==========

NOTES:
- BST property: A node's left subtree value is always at most its value
- Node x, left(x) =< x. Also right(x) > x

Implementations:


```java
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

    void print(){}
}
```

![alt text](assets/InOrderTraversalBinaryTree.jpg "Inorder traversal")
```java
//recursive
void inorder(Node node) {
    if (node != null) {
        inorder(node.left);
        node.print();
        inorder(node.right);
    }
}

//iterative
void inorder(Node root) {
    Stack<Node> stack = new Stack<>();
    Node current = root;
    while (!stack.isEmpty() || current != null) {
        if (current != null) {
            stack.push(current);
            current = current.left;
        } else {
            Node n = stack.pop();
            n.print();
            current = n.right;
        }   
    }
}

//recursive
//O(h)
Node search(Node root, int value) {
    if (root == null || root.value == value) {
        return root;
    }

    if (value <= root.value) {
        return search(root.left, value);
    } else {
        return search(root.right, value);
    }
}

//iterative
//O(h)
Node search(Node root, int value) {
    if (root == null || root.value == value) {
        return root;
    }

    Node current = root;
    while (current != null && current.value != value) {
        if (value <= current.value) {
            current = current.left;
        } else {
            current = current.right;
        }
    }

    return current;
}

// For max, look right
//O(h)
//recursive
Node min(Node root) {
    if (root == null) {
        return null;
    }

    return min(root.left);
}

//iterative
//O(h)
Node min(Node root) {
    if (root != null) {
        return null;
    }

    while (root.left != null) {
        current = current.left;
    }

    return current;
}

//O(h)
Node successor(Node node) {
    if (node != null && node.left != null) {
        return min(node.right);
    }

    Node p = node.parent;
    while (p != null && node == p.right) {
        node = p;
        p = p.parent;
    }
}

void insert(Node root, Node n) {
    Node current = root;
    Node trailer;
    while (current != null) {
        trailer = current;
        if (n.value <= current.value) {
            current = current.left;
        } else {
            current = current.right;
        }
    }

    n.parent = trailer;
    if (trailer == null) {
        root = n
    } else if (n.value < trailer.value) {
        trailer.left = n;
    } else {
        trailer.right = n;
    }
}

Node delete(Node root, int key) {
    if (root == null) return root;
    if (key < root.key) {
        root.left = deleteNode(root.left, key);
    } else if (key > root.key) {
        root.right = deleteNode(root.right, key);
    } else {
        if (root.left == null) {
            return root.right;
        } else if (root.right == null) {
            return root.left;
        }

        root.key = min(root.right);
        // Delete the inorder successor
        root.right = delete(root.right, root.key);
    }
}
```


