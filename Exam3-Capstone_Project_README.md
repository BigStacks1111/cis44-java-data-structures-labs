Project Design Document – Intelligent Cache (LRU Cache)
Capstone Project CIS044 – Data Structures
Michael Nepote
Track: Option C – The Intelligent Cache (Hash Tables & Lists)
1. Problem Overview

Modern web browsers must load frequently visited pages instantly. Users expect near-zero delay when opening tabs like Gmail, YouTube, or Google Docs. However, browsers cannot store unlimited data—cache memory is limited.

Therefore, browsers rely on an LRU Cache (Least Recently Used Cache) to store only the most relevant items while evicting older ones efficiently.

2. Why an LRU Cache? (Real-World Context)

Websites often require resources such as:

HTML files

Images and icons

Stylesheets (CSS)

Scripts (JavaScript)

To improve performance, browsers store recently accessed resources in a cache. When memory is full, the browser must remove something.

The LRU policy says:

Evict the item that has not been used for the longest time.

This matches typical user behavior: recently used pages are more likely to be used again.

3. Data Structure Choice

LRU Cache requires both:

1) Fast lookup → O(1)

Achieved using:

HashMap<K, Node>
Allows instant checking if an item exists in cache.

2) Fast insertions/removals in the middle → O(1)

Achieved using:

Doubly Linked List
Allows instant:

Move-to-front (mark as recently used)

Remove tail (evict least recently used)

UML Diagram

+--------------------------+
|       LRUCache<K, V>     |
+--------------------------+
| - capacity: int          |
| - map: HashMap<K, Node>  |
| - head: Node             |
| - tail: Node             |
+--------------------------+
| + get(key: K): V         |
| + put(key: K, value: V)  |
| - removeNode(n: Node)    |
| - addToFront(n: Node)    |
+--------------------------+

           1        * 
LRUCache ------------------> Node
                   contains

+--------------------------+
|         Node             |
+--------------------------+
| - key: K                 |
| - value: V               |
| - prev: Node             |
| - next: Node             |
+--------------------------+

The expected runtime efficiency of the LRU cache design comes from combining a HashMap with a doubly linked list, allowing all major operations to run in constant time.
A HashMap provides direct access to cached items in O(1) time, while the doubly linked list maintains the usage order so that recently accessed items can be moved to the
front and least recently used items can be removed from the tail, also in O(1) time. Because no traversal or shifting of elements is required, 
both the get and put operations avoid linear-time behavior. 
This structure ensures that the cache consistently maintains its eviction policy while meeting the performance needs of real-time applications such as web browsers.
