Trie
========================

Implementations:
[Trie]
```
class Node {
    Character character;
    Map<Character, Node> children;
    Boolean isLeaf;
    public Node(Character character) {
        this.character = character;
    }
}
class Trie {
    Node root;
    public Trie() { 
        root = new Node();
    }
    void insert(String word) {
        Map<Character, Node> children = root.children;
        for (int i = 0; i < word.length(); i++) {
            Character c = word.charAt(i);
            Node current;
            if (children.containsKey(c)) {
                current = children.get(c);
            } else {
                current = new Node(c);
                children.put(c, current);
            }
            children = current.children;
            if (i == word.length() - 1) {
                current.isLeaf = true;
            }
        }
    }
    Node search(String word) {
        Map<Character, Node> children = root.children;
        Node current;
        for (int i = 0; i < word.length(); i++) {
            Character c = word.charAt(i);
            if (children.containsKey(c)) {
               current = children.get(c);
               if (i == word.length() - 1) {
                   current.isLeaf = true;
               }
               children = current.children;
            } else {
               return null; 
            }
        } 
        return current;
    }
    boolean search(String word) {
        Node node = search(word);
        return node == null && node.isLeaf;
    }
    boolean startsWith(String word) {
        return node == null;
    }
}
```
[/Trie]
