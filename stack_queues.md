Stacks & Queues

PROPERTIES:

- Stacks & Queues are dynamic sets
- Stack => LIFO (Last In First Out)
- Queues => FIFO (First In First Out)

Implimentation #1: Using an Array

//stack of Integers


class Stack{

	int [] s;
	
	int top = -1;
	
	public Stack(int max){
		s = new Int[max];
	}
	
	boolean isEmpty(){
		return top < 0;
	}
	
	void push(int data){
		s[++top] = data;
	}
	void pop(){
		return s[top--];
	}
	
}

Implimentation #2: Using a linkedlist

class Stack{
	int n;
	Node first;
	
	class Node{
		int data;
		Node next;
		public Node(int d, Node t){
			data = d;
			next = t;
		}
	}
	
	boolean isEmpty(){
		return first == null;
	}
	int size(){
		return n;
	}
	void push(int data){
		Node current = first;
		first = new Node(data);
	}
	

}
SUMMARY:
	1. 	void add(Node head, int data)
	
	
	