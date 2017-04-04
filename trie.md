Trie
========================

Implementations:

```java
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
        Node current = null;
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
        return node != null && node.isLeaf;
    }
    
    boolean startsWith(String word) {
        Node node = search(word);
        return node != null;
    }
}
```

```python
class Node:
  def __init__(self, character):
    self.character = character
    self.children = {}
    self.isLeaf = False
    
  def __repr__(self):
    return self.character + " -> " + str(self.children)

class Trie:
  def __init__(self):
    self.root = Node("")
    
  def __str__(self):
    return str(self.root)
    
  def insert(self, word):
    children = self.root.children
    for index, c in enumerate(word):
      current = None
      if c in children.keys():
        current = children[c]
      else:
        current = Node(c)
        children[c] = current
        
      if index == len(word) - 1:
          current.isLeaf = True
        
      children = current.children
  
  def search(self, word):
    node = self.doSearch(word)
    return node is not None and node.isLeaf
    
  def startsWith(self, word):
    return self.doSearch(word) is not None
    
  def doSearch(self, word):
    children = self.root.children
    current = None
    for c in word:
      if c in children.keys():
        current = children[c]
        children = current.children
      else:
        current = None
    
    return current
```
