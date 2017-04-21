Stacks & Queues

PROPERTIES:

- Stacks & Queues are dynamic sets
- Stack => LIFO (Last In First Out)
- Queues => FIFO (First In First Out)

Implementation #1: Using an Array

//stack of Integers

```java
class Stack {
	int [] s;
	int top = -1;
	
	public Stack(int max) {
		s = new Int[max];
	}
	
	boolean isEmpty() {
		return top < 0;
	}
	
	void push(int data) {
		s[++top] = data;
	}

	void pop() {
		return s[top--];
	}
}
```

Implementation #2: Using a Linked list

```java
class Stack {
    int n;
    Node first;
    
    class Node {
        int data;
        Node next;
        public Node(int d, Node t) {
            data = d;
            next = t;
        }
        
        public String toString() {
          return data + "->" + next;
        }
    }
    
    boolean isEmpty() {
        return first == null;
    }
    
    int size() {
        return n;
    }
    
    void push(int data) {
      if (first == null) {
          first = new Node(data, null);
      } else {
        first.next = new Node(data, null);
      }
    }
    
    int pop() {
      Node current = first;
      while (current.next != null) {
        current = current.next;
      }
      
      int data = current.data;
      
      current = null;
      return data;
    }
    
    public String toString() {
      return first.toString();
    }
}

//Implementation #1: Using an Array
interface Queue<T> {
    void enqueue(T data);
    T dequeue();
    boolean isEmpty();
}

class Queue<T> implements Queue<T> {
    T[] data;
    int first, last = 0;
    int defaultSize = 10;
    Queue() {
        data = new T[defaultSize];
    }

    boolean isEmpty() {
        return last == 0;
    }
    int size() {
        return last + 1;
    }

    void resize() {
        T[] tmp = new T[data.length * 2];
        int i = 0;
        Arrays.fill(tmp, data[i++]);
        data = tmp;
    }

    void enqueue(T data) {
        if (last >= data.length -1 ) {
            resize();
        }

        data[last++];
    }

    T dequeue() {
        if (isEmpty()) return null;
        return data[first++];
    }
}

//Implementation #2: Using a Linked list
class Queue<T> {
    class Node {
        T data;
        Node next;
    }
    
    Node first, last;
    int total;
    void enqueue(T data) {
        Node current = last;
        last = new Node();
        last.data = data;
        if (total++ == 0 ) first = last;
        else current.next = last;
    }
    T dequeue() {
        if (total <= 0) return null;
        T data = first.data;
        first = first.next;
        if (--total == 0) last = null;
        return data;
    }
}
```