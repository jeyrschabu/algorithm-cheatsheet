HashMaps
==========

NOTES:
- Open Addressing, Chaining, Linear Probe
- Avoid collisions using Chaining
- O(n) for worst case scenario for insertion, search and delete

Implementations (integer dictionary):

```
class HashMap <K, V> {
	private Entry[] table;
	int total;
	class Entry {
		K key;
		V value;
		Entry(K key, V value) {
			this.key = key;
			this.value = value;
		}
	}
	HashMap() {
		table = new Entry[10];
		total = 0;
	}
	void resize() {
		Entry [] tmp = new Entry[table.length * 2];
		int i = 0;
		Arrays.fill(tmp, table[i++]);
		table = tmp;
	}
	boolean containsKey(Key key) {
		int hash = key.hashCode() % total;
		while (table[hash] != null && table[hash].key != key) {
			hash = (hash + 1) % total;
		}
		return Objects.equals(table[hash].key, key);
	}
    boolean remove(Key key) {
        int hash = key.hashCode() % total;
        while (table[hash] != null && table[hash].key != key) {
            hash = (hash + 1) % total;
        }
        if (Objects.equals(table[total].key, key)) {
            table[total--] = null;
            return true;
        }
        return false;
    }
	void put(K key, V value) {
		if (total++ >= table.length - 1) {
			resize();
		}
		int hash = key.hashCode() % total;
		while (table[hash] != null && table[hash].key != key) {
			hash = (hash + 1) % total;
		}
		table[hash] = new Entry(key, value);
	}
	void get(K key) {
		int hash = key.hashCode() % total;
		while (table[hash] != null && table[hash].key != key) {
			hash = (hash + 1) % total;
		}
		return table[hash];
	}	
}
```

OR

```
class HashMap<K, V> {
    final static int MAX = 128;
    Entry[] table;
    HashMap() {
        table = new Entry[MAX];
    }
    void put(K key, V value) {
        int hash = key.hashCode() % MAX;
        if (table[hash] == null) {
            table[hash] = new Node(key, value, null);
        } else {
            Node current = table[hash];
            while (current.next != null && current.key != key) {
                current = current.next;
            }
            if (current.key == key) 
                current.value = value;
            }else {
                current.next = new Node(key, value, null);
            }
        }
    }
    V get(K key) {
        int hash = key.hashCode() % MAX;
        if (table[hash] == null) return null;
        Node current = table[hash];
        while (current.next != null && current.key != key) current = current.next;
        return (current.key == key) ? current.value ; null;
    }
    void remove(K key) {
        int hash = key.hashCode() % MAX;
        if (table[hash] == null) return;
        Node current = table[hash];
        Node previous = null;
        while (current.next != null && current.key != key) {
            previous = current;
            current = current.next;
        }
        if (current.key == key) {
            if (previous == null) table[hash] = current.next;
            else previous.next = current.next;
        }
    }
    class Node {
        K key;
        V value;
        Node next;
        Node (K key, V value, Node next) {
            this.key = key;
            this.value = value;
            this.next = next;
        }
    }
}
```

Operations:
- search(D, k): Given a key k, return a pointer to the element in the dictionary D whose key value is k, if one exists

