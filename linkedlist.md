LinkedList
==========

- void add(Node head, int data)
- boolean search(Node head, int data)
- boolean remove(Node head, Node previous, int data)
- Node reverse(Node node)
- Node printNthToLast(Node head, int n)
- Node reverseNthNodeFromLast(Node head, int n)
- Node mergeSortedList(Node l1, Node l2)
- Node removeDuplicates(Node head)
- boolean removeRestricted(Node node, int data)
- Node partitionList(Node head, int data)
- Node sumTwoLists(Node first, Node last)
- boolean hasCycle(Node head)
- Node firstNodeInLoop(Node head)
- boolean isPalindrome(Node head)

```
class Node {
	int data;
	Node next;
	public Node(int data) {
		this.data = data;
		this.next = null;
	}
}
```

[ADD]

- iterative
```
void add(Node head, int data) {
	Node current = head;
	if (current == null) {
		current = new Node(data, null);
		head = current;
	} else {
	  	while(current.next != null) current = current.next;
	  	current.next = new Node(data, null);
	}
}
```
- recursive

```
void add(Node head, int data) {
	Node current = head; 
	if (current == null) {
		current = new Node(data);
		head = current;
		return;
	}
	add(current.next, data);
}
```

```
//add first
void addFirst(int data, Node head) {
	Node current = new Node(data);
	current.next = head;
	//update the head
	head = current;
}
```
[/ADD]

[SEARCH]
```
//Recursive
boolean search(Node head, int data) {
	Node  current = head;
	if (current == null) return false;
	if (current.data == data) return true;
	return search(current.next, data);
}
```

```
//Iterative
boolean search(Node head, int data) {
	boolean found = false;
	Node current = head;
	while (current != null && current.data != data) {
		current = current.next;
	}
	return current != null;
}
```

[/SEARCH]

[REMOVE]

```
//iterative
boolean remove(Node head, int data) {
	if (head == null) return false;
	if (head.data == data) head = head.next;
	Node current = head;
	Node previous = null;
	while(current != null && current.data != data) {
		previous = current;
		current = current.next;
	}
	if (current == null) return false;
	previous.next = current.next;
	return true;
}
```

```
//recursive
boolean remove(Node head, Node previous, int data) {
	Node current = head;
	if(current == null) return false;
	if(current.data == data ) {
		if (previous == null) {
			current = current.next;
			head = current;
			return true;
		} else {
			previous.next = current.next;
		}
	}
	return remove(current, current.next, data);
}
```
[/REMOVE]


[REVERSE]

```
//iterative
Node reverse(Node head) {
	Node current = head;
	Node next;
	Node previous = null;
	while (current != null) {
		next = current.next;
		current.next = previous;
		previous = current;
		current = next;
	}
	head = previous;
	return head;
}

Node reverse(Node head) {
    if (head == null || head.next == null) return head;
    Node remain = reverse(head.next);
    Node current = remain;
    while(current.next != null) current = current.next;
    current.next = head;
    head.next = null;
    return remain;
}
```

```
//recursive
Node reverse(Node head) {
	if ( head == null || n.next == null) return head;
	Node r = reverse(head.next);
	head.next.next = head;
	head.next = null;
	return r;
}
```
[/REVERSE]

[GET Nth TO LAST]

```
//runner pointer method
Node getNthToLast(Node head, int n) {
	Node p1 = head;
	Node p2 = head;
	int count = 0;
	while (count++ < n) {
		if(p2 == null) return;
		p2 = p2.next;
	}
	while (p2 != null) {
		p1 = p1.next;
		p2 = p2.next;
	}
	return p1;
}
```

```
//version 2: get the length of the list and get the offset with n
Node getNthToLast(Node head, int n) {
	int len = 0;
	Node current = head;
	while (current != null) {
		++len;
		current = current.next;
	}
	current = head;
	if (len < n) return;
	int offSet = len - n + 1;
	for (int i = 0; i < offSet; i++) current = current.next;
	return current;
}
```
[/GET Nth TO LAST]

[REVERSE Nth TO LAST]

```
Node reverseNthNodeFromLast(Node head, int n) {
	//first find the nth node (see getNthToLast)
	int counter = 0, i = 0;
	Node p1 = head, p2 = head;
	while (counter++ < n) {
		if (p2 == null) return null;
		p2 = p2.next;
	}
	while (p2 != null) {
		p1 = p1.next;
		p2 = p2.next;
		i++; //we care about this index
	}
	//p1 is the node we want
	Node current = p1, previous = null, next;
	while (current != null) {
		next = current.next;
		current.next = previous;
		previous = current;
		current = next;
	}
	current = previous;
	if (i <= 0) return current;
	//attach the beginning of the lost to the reverse position
	Node tmp = head;
	while (--i > 0) tmp = tmp.next;
	tmp.next = current;
	return head;
}
```

[/REVERSE Nth TO LAST]

[MERGE TWO SORTED LIST]

```
//iterative
Node mergeSortedList(Node l1, Node l2) {
	Node p1 = l1, p2 = l2;
	Node fakeHead = new Node(-1);
	Node p = fakeHead;
	while (p1 != null && p2 != null) {
		if (p1.data <= p2.data) {
			p.next = p1;
			p1 = p1.next;
		} else {
			p.next = p2;
			p2 = p2.next;
		}
		p = p.next;
	}
	if (p1 != null) p.next = p1;
	if (p2 != null) p.next = p2;
	return fakeHead;
}
```

```
//recursive (more intuitive)
Node mergeSortedList(Node l1, Node l2) {
	Node result = null;
	if (l1 == null) return l2;
	if (l2 == null) return l1;	
	if (l1.data <= l2.data) {
		result = l1;
		result.next = mergeSortedList(l1.next, l2);
	} else {
		result = l2;
		result.next = mergeSortedList(l1, l2.next);
	}
	return result;
}
```

[/MERGE TWO SORTED LIST]

[REMOVE DUPS]
```
//Note: this can written using a while loop as well, the same approach can be used to detect dups. 
//The method would return a boolean
Node removeDuplicates(Node head) {
	for (Node i = head, i != null ; i = i.next)
		for (Node j = i.next; j != null; j = j.next)
			if (i.data == j.data) i.next = j.next;
	return head;
}
```
[/REMOVE DUPS]

[REMOVE RESTRICTED]

```
//Note: remove a node if only given access to that node
//assumption: this is not the last node in the list
boolean removeRestricted(Node node, int data) {
	Node next = node.next;
	node.data = next.data;
	node.next = next.next;
	return true;
}
```
[/REMOVE RESTRICTED]

[PARTITION]

```
//Note: Create two separate lists that are sorted around data
//Partition a list around x such that all nodes before are less than x and the ones after are greater than
Node partitionList(Node head, int data){
	Node l1 = new Node(-1);
	Node l2 = new Node(-1);
	Node n = l1, m = l2;
	Node current = head;
	while (current != null) {
		if (current.data <= data)
			n.next = new Node(data);
			n = n.next;
		} else {
			m.next = new Node(data);
			m = m.next;
		}
		current = current.next;
	}
	//now we have m & n perfectly sorted with fake heads. lets move them one step
	n = n.next;
	m = m.next;
	//get l1 which uses n as a runner to link to m
	Node tmp = l1;
	while (tmp.next != null) tmp = tmp.next;
	tmp.next = m;
	return l1;
}
```
[/PARTITION]

[SUM TWO LISTS]

```
Node sumTwoLists(Node first, Node last) {
	Node res = null;
	Node tmp, prev = null;
	int carry = 0; sum;
	while (first != null && second != null) {
		int left = (first != null ) ? first.data : 0;
		int right = (last != null ) ? last.data : 0;
		sum  = left + right + carry;
		carry = (sum >= 0) ? 1 : 0;
		sum %=10;
		tmp = new Node(sum);
		if (res == null) {
			res = tmp;
		} else {
			prev.next = tmp;
		}
		prev = tmp;
		if (first != null) first = first.next;
		if (last != null) last = last.next;
	}
	if (carry > 0) tmp.next = new Node(carry);
	return res;
}
```
[/SUM TWO LISTS]

[HAS CYCLE]

```
//Note: using Floyd Cycle Detection Algorithm
//given a finite set S with elements xi...xn
//x0, x1 = f(x0), x2 = f(x1) ... xi = f(xi - 1)
//The sequence of iterated functions must use the same values twice
//Complexity : O(1) in space, O(n) in complexity
//hare-tortoise algorithm: hare is always  faster than the hare and will keep seeing the turtle if there is a cycle
boolean hasCycle(Node head) {
	Node slow = head, fast = head;
	while (slow != null && fast.next != null) {
		slow = slow.next;
		fast = fast.next.next;
		if (slow == fast) return true;
	}
	return false;
}
```
[/HAS CYCLE]

[FIRST NODE IN LOOP]

```
//Note : uses Floyd cycle detection algorithm, then advances the nodes correctly to detect the first node in the loop
//returns null if there are no loops
Node firstNodeInLoop(Node head) {
	Node slow = head, fast = head;
	while (fast != null && fast.next != null) {
		slow = slow.next;
		fast = fast.next.next;
		if(slow == fast) break;
	}
	if (fast == null || fast.next == null) return null;
	slow = head;
	while (slow != fast) {
		slow = slow.next;
		fast = fast.next;
	}
	return fast;
}
```
[/FIRST NODE IN LOOP]

[PALINDROME]

```
//Note: Solution #1 uses a stack as a buffer O(1) space, O(n) Complexity. Uses property of a stack: 
// elements get popped up in reverse order from how they were inserted
boolean isPalindrome(Node head) {
	Stack<Integer> stack = new Stack<Integer>();
	Node current = head;
	while (current != null) {
		stack.push(current.data);
		current = current.next;
	}
	current = head;
	while (current != null) {
		if (stack.pop() != current.data) return false;
		current = current.next;
	}
	return true;
}
```

```
//Note: Solution #2 reverses the list from the middle and compare the two lists
boolean isPalindrome(Node head) {
	Node current = head;
	int len = 0;
	while (current != null) {
		current = current.next;
		len++;
	}
	current = head;
	int n = len/2, i = 0;
	while (i++ <= n) current = current.next;
	//now reverse it
	Node previous = null, next;
	while (current != null) {
		next = current.next;
		current.next = previous;
		previous = current;
		current = next;
	}
	Node first = head, second = previous;
	while(first != null && second != null){
		if(first.data != second.data) return false;
		first = first.next;
		second = second.next;
	}
	return true;
}
```
[/PALINDROME]
