# Comprehensive Data Structures & Algorithms Mastery Guide
*For Industry Professionals: Junior to Staff Engineer Levels*

## Table of Contents
1. [Recursion Types and Patterns](#recursion-types-and-patterns)
2. [Foundational Data Structures](#foundational-data-structures)
3. [Tree Structures](#tree-structures)
4. [Heap Structures](#heap-structures)
5. [Hash-Based Structures](#hash-based-structures)
6. [Graph Structures & Representations](#graph-structures-and-representations)
7. [Fundamental Algorithms](#fundamental-algorithms)
8. [Graph Algorithms](#graph-algorithms)
9. [Dynamic Programming](#dynamic-programming)
10. [Greedy Algorithms](#greedy-algorithms)
11. [Divide and Conquer](#divide-and-conquer)
12. [Backtracking & Branch-and-Bound](#backtracking-and-branch-and-bound)
13. [String Algorithms](#string-algorithms)
14. [Mathematical Algorithms](#mathematical-algorithms)
15. [Advanced Algorithm Design](#advanced-algorithm-design)
16. [System-Level Algorithms](#system-level-algorithms)
17. [Experience Level Roadmap](#experience-level-learning-roadmap)

---

## Recursion Types and Patterns

Recursion is a cornerstone of algorithmic problem-solving. Below is a comprehensive overview of recursion types and patterns with additional fields for clarity.

| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Direct Recursion** | Function calls itself directly to solve a problem. | Calculating factorial (n!). | O(n) | O(n) stack | Simple to implement. | Stack overflow for large n. |
| **Indirect Recursion** | Function A calls B, which calls A. | Parsing nested expressions in compilers. | O(n) | O(n) stack | Models mutual dependencies. | Complex to debug. |
| **Tail Recursion** | Recursive call is the last operation. | Summing a list of numbers. | O(n) | O(1) with TCO | Memory-efficient with TCO. | Requires compiler TCO support. |
| **Non-Tail Recursion** | Processing after recursive call. | Fibonacci number calculation. | O(2^n) naive | O(n) stack | Intuitive for tree problems. | Inefficient without optimization. |
| **Linear Recursion** | Single recursive call per invocation. | Linked list traversal. | O(n) | O(n) stack | Simple control flow. | Stack depth issue. |
| **Binary Recursion** | Two recursive calls per invocation. | Binary tree preorder traversal. | O(n) | O(log n) stack | Natural for binary trees. | Higher memory usage. |
| **Multiple Recursion** | More than two recursive calls. | N-ary tree traversal. | O(n) | O(log n) stack | Flexible for complex trees. | Increased complexity. |
| **Mutual Recursion** | Functions call each other recursively. | State machine in lexical analysis. | O(n) | O(n) stack | Models state transitions. | Hard to maintain. |
| **Nested Recursion** | Recursive call’s argument is recursive. | Ackermann function. | O(2^n) | O(n) stack | Theoretical modeling. | Impractical for large inputs. |
| **Tree Recursion** | Multiple branching recursive calls. | Generating combinations. | O(2^n) | O(n) stack | Solves combinatorial problems. | Exponential time cost. |
| **Excessive Recursion** | Inefficient recursion causing overflow. | Naive Fibonacci (anti-pattern). | O(2^n) | O(n) stack | None (avoid). | Performance bottleneck. |
| **Primitive Recursion** | Result depends on previous result. | Arithmetic sequence generation. | O(n) | O(n) stack | Predictable patterns. | Limited flexibility. |
| **Structural Recursion** | Follows input data structure. | JSON object processing. | O(n) | O(n) stack | Matches data hierarchy. | Stack depth issue. |
| **Generative Recursion** | Generates new data during recursion. | Merge sort subproblems. | O(n log n) | O(n) stack | Efficient for D&C. | Complex to design. |
| **Backtracking Recursion** | Explores paths, backtracks on failure. | N-Queens solver. | O(n!) | O(n) stack | Solves constraint problems. | Exponential time. |
| **Infinite Recursion** | Lacks base case, causes errors. | Debugging recursive loops. | Infinite | Infinite | None (avoid). | Crashes program. |
| **Head Recursion** | Recursive call before operations. | Reverse linked list printing. | O(n) | O(n) stack | Intuitive for post-processing. | Memory-intensive. |
| **Tail-End Recursion** | Tail recursion with explicit returns. | Graph traversal optimization. | O(n) | O(1) with TCO | Optimized memory use. | TCO dependency. |
| **Corecursion** | Builds results lazily. | Infinite stream generation. | O(n) | O(1) | Lazy evaluation. | Language-specific support. |
| **Anonymous Recursion** | Recursion in anonymous functions. | Lambda-based functional code. | O(n) | O(n) stack | Compact code. | Harder to read. |
| **Hybrid Recursion** | Mixes iterative/recursive logic. | Hybrid tree traversal. | O(n) | O(log n) stack | Balances performance. | Increased complexity. |
| **Memoized Recursion** | Caches results for efficiency. | Dynamic programming shortest path. | O(n) with cache | O(n) cache | Avoids recomputation. | Cache overhead. |
| **Divide and Conquer** | Splits, solves, combines subproblems. | Quick sort implementation. | O(n log n) | O(log n) stack | Scalable for large data. | Overhead in combining. |
| **Dynamic Programming Recursion** | Optimized with memoization/tabulation. | Longest common subsequence. | O(n²) | O(n²) | Efficient for overlapping problems. | Space overhead. |
| **Contextual Recursion** | Adapts logic based on input/state. | Recursive descent parsing. | O(n) | O(n) stack | Flexible for parsing. | State management complexity. |

---

## Foundational Data Structures

### Linear Data Structures

#### Arrays & Dynamic Arrays
| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Static Arrays** | Fixed-size contiguous memory. | Pixel data in images. | O(1) access | O(n) | Cache-friendly. | Fixed size. |
| **Dynamic Arrays** | Resizable arrays (e.g., Python lists). | User input list in forms. | O(1) amortized append | O(n) | Flexible sizing. | Resizing overhead. |
| **Resizing Strategies** | Doubling or 1.5x growth for arrays. | Text editor buffer expansion. | O(1) amortized | O(n) | Efficient growth. | Temporary over-allocation. |
| **Multi-dimensional Arrays** | Arrays of arrays (row/column-major). | Matrix operations. | O(1) access | O(n^m) | Structured data. | Memory overhead. |
| **Sparse Arrays** | Compressed sparse data storage. | Large zero-heavy matrices. | O(log n) access | O(k) (k non-zeros) | Saves space. | Complex access. |
| **Circular Arrays** | Wrapped array as ring buffer. | Streaming data buffer. | O(1) enqueue/dequeue | O(n) | Efficient reuse. | Fixed capacity. |
| **Memory-mapped Arrays** | Disk-mapped arrays for large data. | Bioinformatics datasets. | O(1) access | O(n) disk | Handles large data. | I/O latency. |
| **SIMD-optimized Arrays** | Arrays for vectorized operations. | ML parallel processing. | O(1) per op | O(n) | High performance. | Hardware dependency. |

#### Strings & Text Processing
| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **String Representations** | C-style or length-prefixed strings. | User input storage. | O(n) traversal | O(n) | Simple storage. | Encoding issues. |
| **Unicode Handling** | UTF-8, UTF-16 encoding support. | Multilingual text rendering. | O(n) processing | O(n) | Global text support. | Encoding complexity. |
| **String Interning** | Reuses identical strings. | Compiler symbol tables. | O(1) lookup | O(n) | Memory efficiency. | Overhead in setup. |
| **StringBuilder Patterns** | Efficient string concatenation. | Dynamic SQL query building. | O(1) amortized append | O(n) | Fast concatenation. | Not thread-safe. |
| **Text Segmentation** | Splits text into words/sentences. | NLP tokenization. | O(n) | O(n) | Enables text analysis. | Language dependency. |
| **String Compression** | Run-length or LZ77 compression. | Log file compression. | O(n) | O(n) | Saves storage. | Decompression cost. |
| **Immutable Strings** | Copy-on-write string semantics. | Java thread-safe strings. | O(n) copy | O(n) | Thread safety. | Copy overhead. |
| **String Pooling** | Shared string storage. | JVM string optimization. | O(1) lookup | O(n) | Memory efficiency. | Pool management. |

#### Stacks & Stack Applications
| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Array-based Stacks** | Fixed-size array stacks. | Postfix expression evaluation. | O(1) push/pop | O(n) | Simple implementation. | Fixed capacity. |
| **Linked List Stacks** | Dynamic linked list stacks. | Undo in text editors. | O(1) push/pop | O(n) | Flexible sizing. | Memory overhead. |
| **Expression Evaluation** | Stacks for infix/prefix/postfix. | Compiler expression parsing. | O(n) | O(n) | Handles complex expressions. | Limited to expressions. |
| **Function Call Management** | Manages call stack/frames. | Runtime stack in VMs. | O(1) push/pop | O(n) | Essential for execution. | Stack overflow risk. |
| **Undo/Redo Systems** | Tracks reversible operations. | Graphic design software undo. | O(1) push/pop | O(n) | User-friendly feature. | Memory usage. |
| **Browser History** | Navigation history stack. | Browser back/forward buttons. | O(1) push/pop | O(n) | Simple navigation. | Limited history size. |
| **Parentheses Matching** | Checks balanced brackets. | Code editor syntax check. | O(n) | O(n) | Fast validation. | Limited to brackets. |
| **Stack-based VMs** | Stacks for instruction execution. | JVM bytecode execution. | O(1) per op | O(n) | Portable execution. | Performance overhead. |

#### Queues & Queue Variations
| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Array-based Queues** | Circular buffer queues. | OS task scheduling. | O(1) enqueue/dequeue | O(n) | Efficient access. | Fixed size. |
| **Linked List Queues** | Dynamic front/rear pointers. | Printer job queue. | O(1) enqueue/dequeue | O(n) | Flexible sizing. | Pointer overhead. |
| **Double-ended Queues** | Operations at both ends. | Sliding window algorithms. | O(1) push/pop | O(n) | Versatile access. | Complex implementation. |
| **Priority Queues** | Priority-based ordering. | CPU job scheduling. | O(log n) insert/extract | O(n) | Priority handling. | Overhead vs. regular queues. |
| **Concurrent Queues** | Thread-safe queues. | Producer-consumer patterns. | O(1) amortized | O(n) | Thread safety. | Synchronization cost. |
| **Blocking Queues** | Blocks on empty/full states. | Message passing in systems. | O(1) enqueue/dequeue | O(n) | Robust communication. | Blocking delays. |
| **Work-stealing Deques** | Parallel task distribution. | Parallel framework scheduling. | O(1) amortized | O(n) | Load balancing. | Complex design. |
| **Message Queues** | Inter-process communication. | Event handling in brokers. | O(1) enqueue/dequeue | O(n) | Distributed messaging. | Latency in networks. |

#### Linked Lists & Variations
| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Singly Linked Lists** | One-way node connections. | Music playlist management. | O(n) traversal | O(n) | Dynamic sizing. | No backward traversal. |
| **Doubly Linked Lists** | Bidirectional node connections. | Browser navigation history. | O(n) traversal | O(n) | Flexible navigation. | Extra memory. |
| **Circular Linked Lists** | Circular node connections. | Josephus problem solution. | O(n) traversal | O(n) | Cyclic access. | Complex termination. |
| **Skip Lists** | Probabilistic fast-search lists. | In-memory database lookups. | O(log n) expected | O(n) | Fast search. | Probabilistic balance. |
| **Unrolled Linked Lists** | Multiple elements per node. | Database storage efficiency. | O(n) traversal | O(n) | Cache-friendly. | Complex updates. |
| **XOR Linked Lists** | Memory-efficient using XOR. | Embedded system lists. | O(n) traversal | O(n) | Memory saving. | Complex navigation. |
| **Lock-free Linked Lists** | Concurrent lists without locks. | Concurrent data stores. | O(n) traversal | O(n) | High concurrency. | Complex design. |
| **Persistent Linked Lists** | Immutable functional lists. | Version control data history. | O(n) copy | O(n) | Immutability. | Copy overhead. |

---

## Tree Structures

### Binary Trees & Search Trees

#### Basic Binary Trees
| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Tree Traversals** | Preorder, inorder, postorder, level-order. | Parse tree generation. | O(n) | O(h) stack | Flexible traversal. | Stack usage. |
| **Recursive vs Iterative Traversals** | Stack-based iterative traversal. | Embedded system tree processing. | O(n) | O(h) stack | Memory control. | Complex code. |
| **Tree Construction** | Build from traversals/arrays. | Tree deserialization. | O(n) | O(n) | Reconstructs trees. | Input dependency. |
| **Binary Tree Properties** | Height, depth, balance factor. | AVL tree validation. | O(n) | O(h) stack | Structural analysis. | Full traversal needed. |
| **Thread Binary Trees** | Inorder threading for efficiency. | Non-recursive traversal. | O(n) setup | O(n) | Saves stack space. | Complex setup. |
| **Expression Trees** | Arithmetic expression representation. | Expression evaluation. | O(n) | O(n) | Clear representation. | Limited to expressions. |
| **Decision Trees** | Decision-making tree structure. | ML classification. | O(n) traversal | O(n) | Interpretable models. | Overfitting risk. |
| **Parse Trees** | Syntax structure representation. | Compiler syntax analysis. | O(n) | O(n) | Syntax validation. | Parsing overhead. |

#### Binary Search Trees (BST)
| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **BST Operations** | Insert, delete, search, min/max. | Dictionary lookups. | O(h) (h=height) | O(h) stack | Fast searches. | Unbalanced degradation. |
| **BST Properties** | Inorder yields sorted sequence. | Sorted list generation. | O(n) | O(h) stack | Sorted traversal. | Requires balance. |
| **Deletion Strategies** | Successor/predecessor replacement. | BST maintenance. | O(h) | O(h) stack | Maintains BST property. | Complex logic. |
| **BST Validation** | Verifies BST property. | Debugging BST apps. | O(n) | O(h) stack | Ensures correctness. | Full traversal. |
| **Range Queries** | Finds elements in a range. | Database filtering. | O(h + k) (k=results) | O(h) stack | Efficient ranges. | Balance dependency. |
| **BST to Sorted Array** | Flattens BST to sorted array. | Tree serialization. | O(n) | O(n) | Easy conversion. | Extra space. |
| **Threaded BSTs** | Space-efficient traversal. | Memory-constrained systems. | O(n) setup | O(n) | Saves stack. | Complex updates. |
| **Randomized BSTs** | Treaps with random insertion. | Probabilistic balancing. | O(log n) expected | O(n) | Simple balancing. | Probabilistic. |

#### Self-Balancing Trees
| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **AVL Trees** | Height-balanced with rotations. | Real-time indexing. | O(log n) | O(n) | Guaranteed balance. | Rotation overhead. |
| **Red-Black Trees** | Color-based balancing. | C++ std::map. | O(log n) | O(n) | Robust balancing. | Complex rules. |
| **Splay Trees** | Self-adjusting move-to-root. | Cache optimization. | O(log n) amortized | O(n) | Frequent access speed. | Amortized bounds. |
| **Treaps** | Randomized BST with heap property. | Distributed systems. | O(log n) expected | O(n) | Simple randomization. | Probabilistic. |
| **Scapegoat Trees** | Weight-balanced trees. | Dynamic datasets. | O(log n) amortized | O(n) | Simple maintenance. | Amortized bounds. |
| **AA Trees** | Simplified red-black trees. | Teaching balancing. | O(log n) | O(n) | Simpler than RB trees. | Less optimized. |
| **Weight-balanced Trees** | Size-based balancing. | High-performance searches. | O(log n) | O(n) | Flexible balancing. | Complex updates. |
| **Optimal BSTs** | Minimizes access cost with DP. | Skewed access optimization. | O(n²) build | O(n²) | Optimal access. | High build cost. |

---
## Advanced Tree Structures

Advanced tree structures are critical for specialized applications like databases, file systems, and spatial indexing. Below are the *B-Trees & Variants* and *Specialized Trees* with comprehensive details including **Type**, **Description**, **Example Use Case**, **Time Complexity**, **Space Complexity**, **Key Advantage**, and **Key Limitation**.

### B-Trees & Variants

| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **B-Trees** | Multi-way search trees with multiple keys per node, designed for balanced search. | Database indexing in MySQL. | O(log n) search/insert/delete | O(n) | Efficient for disk-based storage. | Complex implementation. |
| **B+ Trees** | B-trees with linked leaves for efficient range queries. | File system indexing (e.g., NTFS). | O(log n) search, O(log n + k) range | O(n) | Fast range queries. | Higher space overhead. |
| **B* Trees** | B-tree variant with higher node occupancy (2/3 full). | Optimized database indexing. | O(log n) search/insert/delete | O(n) | Better space utilization. | Increased insertion complexity. |
| **2-3 Trees** | B-trees with nodes having 2 or 3 children. | Teaching balanced tree concepts. | O(log n) search/insert/delete | O(n) | Simple balancing rules. | Less flexible than B-trees. |
| **2-3-4 Trees** | B-trees with up to 4 children per node, equivalent to red-black trees. | Internal representation in databases. | O(log n) search/insert/delete | O(n) | Easier to balance than B-trees. | Higher memory per node. |
| **External B-Trees** | B-trees optimized for disk-based storage systems. | Large-scale database storage. | O(log n) I/O operations | O(n) disk | Minimizes disk I/O. | Disk access latency. |
| **Concurrent B-Trees** | B-trees supporting multi-threaded access. | Concurrent database operations. | O(log n) with locking | O(n) | Thread-safe operations. | Synchronization overhead. |
| **Copy-on-Write B-Trees** | B-trees using copy-on-write for updates. | File system snapshots (e.g., Btrfs). | O(log n) search/insert | O(n) | Safe for concurrent snapshots. | High space for updates. |

### Specialized Trees

| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Tries (Prefix Trees)** | Trees storing strings with shared prefixes. | Autocomplete in search engines. | O(m) search/insert (m=string length) | O(ALPHABET_SIZE * n * m) | Fast prefix lookups. | High memory usage. |
| **Compressed Tries** | Tries with merged single-child paths (e.g., Patricia/radix trees). | IP routing tables. | O(m) search/insert | O(n * m) | Reduced space vs. tries. | Complex compression logic. |
| **Suffix Trees** | Compressed tries of all suffixes for pattern matching. | DNA sequence matching. | O(n) build, O(m) search | O(n) | Fast substring search. | High build complexity. |
| **Segment Trees** | Trees for efficient range queries and updates. | Range sum queries in arrays. | O(log n) query/update | O(n log n) | Dynamic range queries. | Space overhead. |
| **Fenwick Trees** | Binary indexed trees for prefix sums. | Cumulative frequency tables. | O(log n) query/update | O(n) | Space-efficient. | Limited to prefix sums. |
| **Interval Trees** | Trees for storing and querying overlapping intervals. | Scheduling conflict detection. | O(log n + k) query (k=overlaps) | O(n) | Efficient interval queries. | Complex updates. |
| **Range Trees** | Trees for multi-dimensional range queries. | Geographic range searches. | O(log^d n + k) query (d=dimensions) | O(n log^d n) | Multi-dimensional queries. | High space complexity. |
| **Quad Trees** | 2D spatial partitioning trees. | Collision detection in games. | O(log n) query/insert | O(n) | Efficient 2D searches. | Limited to 2D spaces. |
| **Octrees** | 3D spatial partitioning trees. | 3D rendering in graphics. | O(log n) query/insert | O(n) | Efficient 3D searches. | High memory for 3D. |
| **K-D Trees** | K-dimensional binary space partitioning. | Nearest neighbor search in ML. | O(log n) query (balanced) | O(n) | Flexible dimensions. | Unbalanced degradation. |
| **R-Trees** | Spatial indexing for rectangular regions. | GIS data indexing. | O(log n) query/insert | O(n) | Efficient spatial queries. | Overlap issues. |
| **LSM Trees** | Log-structured merge trees for write-heavy workloads. | NoSQL databases (e.g., LevelDB). | O(log n) write, O(log n) read | O(n) | High write throughput. | Read amplification. |
| **Merkle Trees** | Cryptographic hash trees for data verification. | Blockchain transaction verification. | O(log n) verification | O(n) | Secure data integrity. | High setup cost. |

---

## Heap Structures

Heap structures are essential for priority queue implementations and sorting algorithms. Below are the *Basic Heaps* and *Advanced Heap Structures* with comprehensive details including **Type**, **Description**, **Example Use Case**, **Time Complexity**, **Space Complexity**, **Key Advantage**, and **Key Limitation**.

### Basic Heaps

| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Binary Heaps** | Tree-based structures satisfying min-heap or max-heap property. | Priority queue in task scheduling. | O(log n) insert/extract, O(1) peek | O(n) | Simple and efficient. | Limited to single priority. |
| **Heap Operations** | Core operations: insert, extract-min/max, decrease-key. | Event-driven simulation. | O(log n) insert/extract, O(log n) decrease-key | O(n) | Fast priority updates. | Requires heap property maintenance. |
| **Heapify Algorithms** | Bottom-up or top-down heap construction. | Building heap from array. | O(n) bottom-up, O(n log n) top-down | O(1) auxiliary | Efficient construction. | Top-down is slower. |
| **Heap Sort** | In-place sorting using a binary heap. | Sorting large datasets. | O(n log n) | O(1) auxiliary | In-place sorting. | Not stable, slower than quicksort. |
| **Priority Queue Implementation** | Heap-based priority queue for dynamic priorities. | Dijkstra’s shortest path algorithm. | O(log n) insert/extract, O(1) peek | O(n) | Efficient priority management. | Overhead vs. simple queues. |
| **Heap Construction** | Building a heap from an unsorted array. | Initializing priority queues. | O(n) | O(1) auxiliary | Linear-time build. | Requires full array scan. |
| **Heap Maintenance** | Restoring heap property after modifications. | Dynamic priority updates. | O(log n) per operation | O(1) auxiliary | Maintains heap invariant. | Repeated operations costly. |
| **D-ary Heaps** | Generalization with d children per node. | High-arity priority queues. | O(log_d n) insert/extract | O(n) | Better cache performance. | Increased child management. |

### Advanced Heap Structures

| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Binomial Heaps** | Forest of binomial trees supporting fast merges. | Network routing algorithms. | O(log n) merge/insert/extract | O(n) | Efficient merging. | Complex structure. |
| **Fibonacci Heaps** | Lazy operations with improved amortized bounds. | Prim’s algorithm for MST. | O(1) insert/decrease-key, O(log n) extract | O(n) | Fast amortized operations. | Complex implementation. |
| **Pairing Heaps** | Simplified alternative to Fibonacci heaps. | Dynamic graph algorithms. | O(1) insert, O(log n) extract (amortized) | O(n) | Simple structure. | Worse worst-case bounds. |
| **Leftist Heaps** | Mergeable heaps with leftist property. | Real-time scheduling systems. | O(log n) merge/insert/extract | O(n) | Fast merging. | Height imbalance issues. |
| **Skew Heaps** | Self-adjusting mergeable heaps. | Incremental graph processing. | O(log n) amortized merge | O(n) | Self-adjusting simplicity. | Amortized bounds only. |
| **Brodal Queues** | Worst-case optimal priority queues. | High-performance systems. | O(1) insert, O(log n) extract | O(n) | Optimal worst-case bounds. | Highly complex. |
| **Rank-Pairing Heaps** | Combines benefits of pairing and rank-based heaps. | Advanced priority queue systems. | O(1) insert, O(log n) extract (amortized) | O(n) | Balanced performance. | Implementation complexity. |
| **Soft Heaps** | Approximate priority queues allowing errors. | Approximate shortest paths. | O(1) insert, O(log n) extract | O(n) | Fast with controlled errors. | Inaccurate results. |

---

## Hash-Based Structures

Hash-based structures are critical for fast lookups and probabilistic data handling. Below are the *Hash Tables & Hash Functions* and *Advanced Hash Structures* with comprehensive details.

### Hash Tables & Hash Functions

#### Hash Function Design
| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Division Method** | Simple modular hashing using division. | Basic hash table keys. | O(1) | O(1) | Simple and fast. | Poor distribution for some inputs. |
| **Multiplication Method** | Uses fractional part of multiplication. | Hashing floating-point keys. | O(1) | O(1) | Better distribution. | Requires careful constant choice. |
| **Universal Hashing** | Family of hash functions to minimize collisions. | Secure hash tables. | O(1) expected | O(1) | Collision resistance. | Setup overhead. |
| **Cryptographic Hash Functions** | Secure hash functions (e.g., SHA family). | Password hashing. | O(n) | O(1) | High security. | Computationally expensive. |
| **Rolling Hash** | Hash updates for sliding windows. | Rabin-Karp string matching. | O(1) per update | O(1) | Efficient substring hashing. | Collision risk. |
| **Perfect Hashing** | Collision-free hash functions for static sets. | Compiler symbol tables. | O(1) lookup | O(n) | Guaranteed O(1) lookup. | Static data only. |
| **Minimal Perfect Hashing** | Space-efficient perfect hashing. | Dictionary storage. | O(1) lookup | O(n) | Minimal space usage. | Complex construction. |
| **Locality-Sensitive Hashing** | Hashes similar items to similar buckets. | Nearest neighbor search in ML. | O(1) expected | O(n) | Approximate similarity search. | Probabilistic accuracy. |

#### Collision Resolution
| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Separate Chaining** | Uses linked lists or arrays for collisions. | General-purpose hash tables. | O(1 + α) expected (α=load factor) | O(n + m) (m=slots) | Simple collision handling. | Memory overhead. |
| **Open Addressing** | Resolves collisions via probing (linear/quadratic). | Cache-efficient hash tables. | O(1/(1-α)) expected | O(m) | Cache-friendly. | Clustering issues. |
| **Double Hashing** | Uses secondary hash for probing. | High-performance hash tables. | O(1/(1-α)) expected | O(m) | Reduced clustering. | Complex hash design. |
| **Robin Hood Hashing** | Reduces probe distance variance. | Low-latency hash tables. | O(1/(1-α)) expected | O(m) | Balanced probe lengths. | Increased insertion time. |
| **Cuckoo Hashing** | Uses multiple hash functions for placement. | Real-time key-value stores. | O(1) worst-case lookup | O(m) | Constant-time lookups. | Rehashing overhead. |
| **Hopscotch Hashing** | Cache-friendly open addressing. | High-performance databases. | O(1) expected | O(m) | Cache efficiency. | Complex neighborhood management. |
| **Consistent Hashing** | Distributes keys across nodes. | Distributed caching (e.g., Redis). | O(log n) with balancing | O(m) | Scalable distribution. | Load imbalance risk. |
| **Rendezvous Hashing** | Alternative distributed hashing. | Load balancing in clusters. | O(k) (k=nodes) | O(m) | Simple node selection. | Higher query cost. |

### Advanced Hash Structures
| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Bloom Filters** | Probabilistic set membership testing. | Cache filtering in databases. | O(1) insert/query | O(m) bits | Space-efficient. | False positives. |
| **Counting Bloom Filters** | Bloom filters with deletion support. | Dynamic set membership. | O(1) insert/delete/query | O(m) bits | Supports deletions. | Higher space usage. |
| **Cuckoo Filters** | Space-efficient alternative to Bloom filters. | Membership testing in networks. | O(1) insert/delete/query | O(m) bits | Deletion and efficiency. | False positives. |
| **Count-Min Sketch** | Estimates frequencies in data streams. | Network traffic monitoring. | O(1) insert/query | O(m) | Handles streaming data. | Overestimation errors. |
| **HyperLogLog** | Estimates cardinality of large sets. | Unique visitor counting. | O(1) insert/query | O(log log n) | Extremely space-efficient. | Approximate results. |
| **Quotient Filters** | Cache-efficient approximate membership. | Database query optimization. | O(1) insert/query | O(m) | Cache-friendly. | False positives. |
| **XOR Filters** | Space-efficient static membership filters. | Static set queries. | O(1) query | O(m) | Minimal space. | Static data only. |
| **Hash Tries** | Combines tries with hashing for key storage. | Fast prefix-based lookups. | O(m) insert/query (m=key length) | O(n * m) | Prefix efficiency. | High memory usage. |

---

## Graph Structures & Representations

Graph structures are fundamental for modeling relationships in various applications, from social networks to routing systems. Below are the *Graph Representations* and *Graph Types & Properties* with comprehensive details including **Type**, **Description**, **Example Use Case**, **Time Complexity**, **Space Complexity**, **Key Advantage**, and **Key Limitation**.

### Graph Representations

| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Adjacency Matrix** | 2D matrix where entry (i,j) indicates an edge from vertex i to j. | Dense graph edge queries in routing. | O(1) edge query, O(V²) traversal | O(V²) | Fast edge checks. | High memory for sparse graphs. |
| **Adjacency Lists** | Array of lists where each list stores neighbors of a vertex. | Social network connections. | O(deg(v)) neighbor query, O(E) traversal | O(V + E) | Memory-efficient for sparse graphs. | Slower edge checks. |
| **Edge Lists** | List of edge tuples (u,v) representing connections. | Kruskal’s MST algorithm. | O(E) edge access, O(E) traversal | O(E) | Simple for edge-based algorithms. | Inefficient neighbor queries. |
| **Incidence Matrix** | Matrix where rows are vertices, columns are edges, indicating relationships. | Network flow analysis. | O(E) edge query | O(V * E) | Clear vertex-edge mapping. | High space complexity. |
| **Compressed Sparse Row (CSR)** | Compact adjacency list format for sparse graphs. | Large-scale graph processing in ML. | O(deg(v)) neighbor query | O(V + E) | Memory and cache efficiency. | Complex setup and updates. |
| **Coordinate Format (COO)** | Triplet list (row, col, value) for sparse matrices. | Sparse matrix operations in scientific computing. | O(E) access | O(E) | Simple sparse representation. | Inefficient for repeated queries. |
| **Graph Compression** | Techniques (e.g., WebGraph) to reduce graph storage. | Web graph storage for search engines. | O(log V) query with compression | O(V + E) compressed | Saves storage for large graphs. | Decompression overhead. |
| **Streaming Graph Representations** | Dynamic structures for evolving graphs. | Real-time social network analysis. | O(1) amortized update | O(V + E) | Handles dynamic graphs. | Complex update management. |

### Graph Types & Properties

| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Directed vs Undirected** | Directed: edges have orientation; undirected: edges are bidirectional. | Web page links (directed) vs. friendships (undirected). | O(V + E) traversal | O(V + E) | Models specific relationships. | Directed graphs need more processing. |
| **Weighted vs Unweighted** | Weighted: edges have costs; unweighted: edges have no costs. | Road networks (weighted) vs. simple connections (unweighted). | O(V + E) traversal | O(V + E) | Captures edge significance. | Increased storage and computation. |
| **Dense vs Sparse** | Dense: many edges; sparse: few edges. | Complete graphs (dense) vs. road networks (sparse). | O(V²) dense, O(V + E) sparse | O(V²) dense, O(V + E) sparse | Dense: fast queries; sparse: low memory. | Dense: high memory; sparse: slower queries. |
| **Connected Components** | Subgraphs where vertices are reachable (strongly/weakly for directed). | Community detection in networks. | O(V + E) DFS/BFS | O(V) | Identifies graph partitions. | Requires full traversal. |
| **Bipartite Graphs** | Vertices split into two sets with edges between sets. | Job assignment problems. | O(V + E) BFS for checking | O(V + E) | Enables matching algorithms. | Limited to two-part structures. |
| **Planar Graphs** | Graphs embeddable in 2D without edge crossings. | Circuit board design. | O(V) planarity test | O(V + E) | Simplifies visualization. | Complex planarity testing. |
| **Trees as Graphs** | Acyclic connected graphs with unique paths. | File system hierarchies. | O(V) traversal | O(V) | Simple structure. | Limited connectivity. |
| **DAGs (Directed Acyclic Graphs)** | Directed graphs with no cycles. | Task scheduling with dependencies. | O(V + E) topological sort | O(V + E) | Enables topological ordering. | No cycle support. |
| **Multigraphs** | Graphs allowing multiple edges between vertices. | Transportation networks with multiple routes. | O(V + E) traversal | O(V + E) | Models multiple connections. | Increased complexity in algorithms. |
| **Hypergraphs** | Edges connect multiple vertices (hyperedges). | Collaborative networks in databases. | O(V + E) traversal | O(V + sum(|e|)) | Flexible multi-vertex relations. | High computational complexity. |

---

### Sorting Algorithms

#### Comparison-Based Sorting
| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Bubble Sort** | Simple exchange sort that repeatedly swaps adjacent elements. | Teaching sorting concepts. | O(n²) | O(1) auxiliary | Easy to implement. | Very slow for large datasets. |
| **Selection Sort** | Finds the minimum element and places it at the beginning. | Small datasets with minimal memory. | O(n²) | O(1) auxiliary | Minimal memory usage. | Quadratic time, not adaptive. |
| **Insertion Sort** | Builds a sorted portion by inserting elements incrementally. | Nearly sorted small lists. | O(n²), O(n) best | O(1) auxiliary | Adaptive and stable. | Inefficient for large data. |
| **Shell Sort** | Gap-based insertion sort with diminishing increments. | Medium-sized datasets. | O(n^1.3) to O(n²) | O(1) auxiliary | Faster than simple sorts. | Not stable, gap choice impacts. |
| **Merge Sort** | Divide-and-conquer stable sort that splits and merges. | External sorting large files. | O(n log n) | O(n) auxiliary | Stable and predictable. | Extra space requirement. |
| **Quick Sort** | Partition-based sort with average-case efficiency. | General-purpose in-memory sorting. | O(n log n) avg, O(n²) worst | O(log n) stack | Fast average case. | Unstable, worst-case slowdown. |
| **Heap Sort** | Uses a binary heap for in-place sorting. | Sorting with guaranteed O(n log n). | O(n log n) | O(1) auxiliary | In-place, no worst-case issues. | Not stable, slower than query. |
| **Tree Sort** | Uses a BST to sort elements via insertions. | Dynamic data with frequent insertions. | O(n log n) avg, O(n²) worst | O(n) | Handles dynamic updates. | Unbalanced tree degrades performance. |

#### Non-Comparison Sorting
| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Counting Sort** | Sorts integers using frequency counts. | Sorting exam scores (0-100). | O(n + k) (k=range) | O(n + k) | Linear time for small ranges. | Limited to small integer ranges. |
| **Radix Sort** | Sorts by processing digits (LSD or MSD). | Sorting large integers or strings. | O(d(n + k)) (d=digits) | O(n + k) | Efficient for fixed-length keys. | Requires stable sub-sort. |
| **Bucket Sort** | Distributes elements into buckets and sorts them. | Sorting floating-point numbers. | O(n + k) avg | O(n + k) | Fast for uniform distributions. | Sensitive to distribution. |
| **Pigeonhole Sort** | Variant of counting sort for distinct keys. | Sorting unique integers in range. | O(n + k) | O(n + k) | Simple for distinct keys. | Requires unique keys in range. |

#### Hybrid & Adaptive Sorting
| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Tim Sort** | Adaptive stable sort combining merge and insertion sort. | Python’s default list sorting. | O(n log n), O(n) best | O(n) auxiliary | Adaptive and stable. | Space overhead for merging. |
| **Intro Sort** | Hybrid of quicksort, heapsort, and insertion sort. | C++ std::sort implementation. | O(n log n) | O(log n) stack | Avoids quicksort’s worst case. | More complex implementation. |
| **Smoothsort** | Adaptive heap sort variant with smoother transitions. | Specialized sorting tasks. | O(n log n), O(n) best | O(1) auxiliary | Adaptive performance. | Complex and less practical. |
| **Patience Sort** | Based on longest increasing subsequence. | Sorting with minimal moves. | O(n log n) | O(n) | Unique approach for sequences. | Not general-purpose. |

### Searching Algorithms

#### Array Searching
| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Linear Search** | Sequentially checks each element. | Unsorted small arrays. | O(n) | O(1) | Simple and no preprocessing. | Inefficient for large data. |
| **Binary Search** | Divide-and-conquer on sorted arrays. | Dictionary lookups. | O(log n) | O(1) iterative | Fast for sorted data. | Requires sorted input. |
| **Interpolation Search** | Estimates position based on data distribution. | Uniformly distributed sorted arrays. | O(log log n) avg, O(n) worst | O(1) | Fast for uniform data. | Poor for skewed distributions. |
| **Exponential Search** | Finds range then applies binary search. | Unbounded sorted arrays. | O(log n) | O(1) | Handles unknown sizes. | Requires sorted input. |
| **Jump Search** | Searches by jumping fixed steps. | Sorted arrays with low memory. | O(√n) | O(1) | Fewer comparisons than linear. | Slower than binary search. |
| **Fibonacci Search** | Uses Fibonacci numbers for division. | Sorted arrays in embedded systems. | O(log n) | O(1) | Avoids division operations. | Slightly slower than binary. |
| **Ternary Search** | Divides array into three parts for unimodal functions. | Finding maximum in unimodal arrays. | O(log₃ n) | O(1) | Works on unimodal functions. | Limited applicability. |

#### String Searching
| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Naive Pattern Matching** | Brute-force comparison of pattern with text. | Small text pattern search. | O(n * m) (m=pattern length) | O(1) | Simple implementation. | Very inefficient. |
| **KMP Algorithm** | Uses prefix table for pattern matching. | Text editor search feature. | O(n + m) | O(m) | Linear time matching. | Preprocessing overhead. |
| **Boyer-Moore** | Skips characters using bad character/good suffix rules. | Large text search (e.g., books). | O(n/m) best, O(n * m) worst | O(k) (k=alphabet size) | Fast for large texts. | Complex preprocessing. |
| **Rabin-Karp** | Uses rolling hash for pattern matching. | Plagiarism detection. | O(n + m) avg, O(n * m) worst | O(1) | Multiple pattern searches. | Hash collision risk. |
| **Z Algorithm** | Linear-time pattern matching using Z-values. | String preprocessing for matching. | O(n + m) | O(n + m) | Linear time preprocessing. | Space overhead. |
| **Aho-Corasick** | Automaton for multiple pattern matching. | Virus signature scanning. | O(n + m + z) (z=matches) | O(m * k) | Multiple patterns at once. | High memory usage. |
| **Suffix Array** | Sorted array of all suffixes for pattern matching. | Full-text search in documents. | O(n log n) build, O(log n) search | O(n) | Versatile string queries. | High build cost. |
| **Manacher’s Algorithm** | Finds all palindromic substrings in linear time. | DNA sequence palindrome detection. | O(n) | O(n) | Linear-time palindrome search. | Limited to palindromes. |

---

## Graph Algorithms

Graph algorithms are essential for solving problems involving networks, such as routing, scheduling, and social network analysis. Below are the *Graph Traversals*, *Shortest Path Algorithms*, *Minimum Spanning Tree*, *Network Flow Algorithms*, and *Advanced Graph Algorithms* with comprehensive details including **Type**, **Description**, **Example Use Case**, **Time Complexity**, **Space Complexity**, **Key Advantage**, and **Key Limitation**.

### Graph Traversals

| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
| --- | --- | --- | --- | --- | --- | --- |
| **Depth-First Search (DFS)** | Stack-based exploration of graph vertices. | Finding connected components. | O(V + E) | O(V) stack | Simple and memory-efficient. | May get stuck in deep paths. |
| **Breadth-First Search (BFS)** | Queue-based level-by-level exploration. | Shortest path in unweighted graphs. | O(V + E) | O(V) queue | Finds shortest paths. | Higher memory usage. |
| **Iterative Deepening** | Depth-limited DFS with increasing limits. | Memory-constrained pathfinding. | O(V + E) | O(d) stack (d=depth) | Memory-efficient. | Repeated explorations. |
| **Bidirectional Search** | Searches from source and target simultaneously. | Fast pathfinding in graphs. | O(b^(d/2)) (b=branching factor) | O(b^(d/2)) | Faster than single-direction. | Requires target node. |
| *A Search*\* | Heuristic-guided pathfinding with cost estimates. | Navigation systems (e.g., GPS). | O(E log V) with heap | O(V) | Optimal with admissible heuristic. | Heuristic design complexity. |
| **Best-First Search** | Greedy exploration using heuristic priority. | AI game pathfinding. | O(E log V) with heap | O(V) | Fast with good heuristic. | Non-optimal paths. |

### Shortest Path Algorithms

| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
| --- | --- | --- | --- | --- | --- | --- |
| **Dijkstra’s Algorithm** | Single-source shortest paths for non-negative weights. | Road network routing. | O((V + E) log V) with heap | O(V) | Optimal for non-negative weights. | Fails with negative weights. |
| **Bellman-Ford** | Single-source shortest paths with negative weights. | Currency arbitrage detection. | O(V \* E) | O(V) | Handles negative weights. | Slower than Dijkstra’s. |
| **Floyd-Warshall** | All-pairs shortest paths for any weights. | City-to-city distance matrix. | O(V³) | O(V²) | Handles all pairs and negative weights. | High time and space complexity. |
| **Johnson’s Algorithm** | All-pairs shortest paths for sparse graphs. | Sparse network analysis. | O(V² log V + V \* E) | O(V²) | Efficient for sparse graphs. | Complex preprocessing. |
| *A Algorithm*\* | Heuristic-based shortest path finding. | Game pathfinding (e.g., NPCs). | O(E log V) with heap | O(V) | Fast with good heuristic. | Heuristic dependency. |
| **Bidirectional Dijkstra** | Two-way Dijkstra for faster shortest paths. | Social network distance queries. | O((V + E) log V) | O(V) | Faster than standard Dijkstra. | Requires target node. |

### Minimum Spanning Tree

| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
| --- | --- | --- | --- | --- | --- | --- |
| **Kruskal’s Algorithm** | Greedy edge-based MST construction. | Network cable layout. | O(E log E) with union-find | O(E) | Simple and edge-focused. | Requires sorting. |
| **Prim’s Algorithm** | Greedy vertex-based MST construction. | Telecom network design. | O((V + E) log V) with heap | O(V) | Efficient for dense graphs. | Vertex-focused complexity. |
| **Borůvka’s Algorithm** | Parallel MST by contracting components. | Distributed network design. | O(E log V) | O(V + E) | Parallelizable. | Complex implementation. |
| **Reverse-Delete Algorithm** | Removes edges to form MST. | Robust network pruning. | O(E log E) | O(V + E) | Useful for edge removal. | Less common, higher complexity. |

### Network Flow Algorithms

| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
| --- | --- | --- | --- | --- | --- | --- |
| **Ford-Fulkerson** | Finds maximum flow using augmenting paths. | Traffic flow optimization. | O(E \* | f | ) ( | f |
| **Edmonds-Karp** | BFS-based Ford-Fulkerson implementation. | Bipartite matching. | O(V \* E²) | O(V + E) | Predictable performance. | Slower than advanced methods. |
| **Dinic’s Algorithm** | Uses blocking flows and level graphs. | High-throughput flow problems. | O(V² \* E) | O(V + E) | Faster for dense graphs. | Complex implementation. |
| **Push-Relabel** | Local optimization for max flow. | Large-scale flow networks. | O(V² \* E) | O(V²) | Efficient for sparse graphs. | Higher space complexity. |

### Advanced Graph Algorithms

| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
| --- | --- | --- | --- | --- | --- | --- |
| **Topological Sorting** | Linearizes vertices in a DAG (Kahn’s or DFS). | Task scheduling with dependencies. | O(V + E) | O(V) | Simple DAG ordering. | Limited to DAGs. |
| **Strongly Connected Components** | Finds strongly connected subgraphs (Kosaraju’s, Tarjan’s). | Social network cluster detection. | O(V + E) | O(V) | Identifies graph structure. | Directed graphs only. |
| **Articulation Points** | Identifies cut vertices in a graph. | Network vulnerability analysis. | O(V + E) | O(V) | Finds critical nodes. | Complex for large graphs. |
| **Bridge Finding** | Identifies cut edges in a graph. | Network link failure detection. | O(V + E) | O(V) | Finds critical edges. | Limited to specific use cases. |
| **Biconnected Components** | Finds 2-connected subgraphs. | Robust network design. | O(V + E) | O(V) | Enhances graph robustness. | Complex computation. |
| **Graph Coloring** | Assigns colors to vertices/edges without conflicts. | Scheduling with conflicts. | O(V \* 2^V) exact, O(V + E) greedy | O(V) | Solves conflict problems. | Exact solution is slow. |
| **Maximum Matching** | Finds maximum edge set without shared vertices. | Job assignment in bipartite graphs. | O(V \* E) bipartite, O(V³) general | O(V + E) | Solves pairing problems. | Complex for general graphs. |
| **Traveling Salesman** | Finds shortest tour visiting all vertices. | Delivery route optimization. | O(n!) exact, O(n²) approx | O(n) | Practical approximations. | Exact solution infeasible for large n. |

---

### Classical DP Problems

| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Fibonacci Numbers** | Computes Fibonacci sequence using memoization or tabulation. | Calculating Fibonacci for large n. | O(n) | O(n) memo, O(1) optimized | Simple introduction to DP. | Limited practical use. |
| **Longest Common Subsequence (LCS)** | Finds longest subsequence common to two sequences. | DNA sequence alignment. | O(n * m) (n,m=sequence lengths) | O(n * m) | Solves sequence alignment. | High space complexity. |
| **Longest Increasing Subsequence (LIS)** | Finds longest increasing subsequence in an array. | Stock price trend analysis. | O(n log n) optimized | O(n) | Efficient with binary search. | Not for all sequence types. |
| **Edit Distance** | Computes minimum operations to transform one string to another. | Spell checker corrections. | O(n * m) | O(n * m) | Flexible string transformations. | Space-intensive. |
| **Knapsack Problem** | Optimizes item selection (0/1, unbounded, bounded variants). | Resource allocation in projects. | O(n * W) (W=capacity) | O(n * W) | Versatile optimization. | Pseudo-polynomial time. |
| **Coin Change** | Finds minimum coins or number of ways to make change. | Vending machine coin dispensing. | O(n * T) (T=target) | O(T) | Solves counting problems. | Limited to integer targets. |
| **Matrix Chain Multiplication** | Finds optimal parenthesization for matrix multiplication. | Optimizing matrix computations. | O(n³) | O(n²) | Minimizes multiplication cost. | High computational cost. |
| **Palindrome Partitioning** | Finds minimum cuts to partition string into palindromes. | Text processing for palindromes. | O(n²) | O(n²) | Efficient palindrome handling. | Space overhead. |
| **Word Break** | Segments string using dictionary words. | Text segmentation in NLP. | O(n²) | O(n) | Solves dictionary-based problems. | Dictionary size impacts. |
| **Wildcard Matching** | Matches strings with wildcard patterns (*, ?). | File pattern matching. | O(n * m) | O(n * m) | Flexible pattern matching. | Space and time intensive. |

### Advanced DP Techniques

| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Digit DP** | Counts numbers satisfying digit-based constraints. | Counting valid numbers in range. | O(d * S) (d=digits, S=states) | O(S) | Handles digit constraints. | Complex state design. |
| **Bitmask DP** | Uses bit manipulation for subset enumeration. | Traveling Salesman Problem. | O(n * 2^n) | O(2^n) | Efficient subset handling. | Exponential space/time. |
| **Tree DP** | Applies DP on tree structures for optimization. | Tree diameter calculation. | O(V) (V=vertices) | O(V) | Natural for tree problems. | Tree-specific applicability. |
| **DP on DAGs** | Solves longest/shortest paths in directed acyclic graphs. | Critical path in project scheduling. | O(V + E) | O(V) | Efficient for DAGs. | Limited to acyclic graphs. |
| **Interval DP** | Optimizes solutions over intervals. | Matrix chain multiplication variant. | O(n³) | O(n²) | Solves interval problems. | High complexity. |
| **Profile DP** | Compresses states for multidimensional problems. | Game board state optimization. | O(n * S) (S=compressed states) | O(S) | Reduces state space. | Complex state encoding. |
| **Convex Hull Optimization** | Uses convex hull trick for DP optimization. | Task scheduling with costs. | O(n log n) | O(n) | Fast for monotonic functions. | Requires monotonicity. |
| **Divide and Conquer DP** | Exploits optimal substructure with D&C. | Range query optimization. | O(n log n) | O(n) | Reduces computation. | Complex to implement. |

### State Space Optimization

| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Space-Optimized DP** | Reduces memory usage in DP tables. | LCS with reduced space. | O(n * m) | O(min(n, m)) | Saves memory. | May complicate code. |
| **Rolling Array Technique** | Uses fixed-size array for table DP. | Fibonacci with constant space. | O(n) | O(1) | Constant space usage. | Limited to sequential access. |
| **State Compression** | Represents states efficiently (e.g., bitmasks). | Bitmask DP for TSP. | O(n * 2^n) | O(2^n) | Reduces state storage. | Exponential states. |
| **Coordinate Compression** | Maps large ranges to smaller indices. | Range queries with large values. | O(n log n) preprocessing | O(n) | Handles large ranges. | Preprocessing overhead. |
| **Offline Processing** | Processes queries in batch for efficiency. | Batch range sum queries. | O(n + q log q) (q=queries) | O(n) | Efficient query handling. | Requires all queries upfront. |

---

### Classical Greedy Problems

| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Activity Selection** | Maximizes non-overlapping interval activities. | Scheduling lectures in a classroom. | O(n log n) | O(1) | Simple and optimal. | Limited to non-overlapping intervals. |
| **Fractional Knapsack** | Maximizes value in a knapsack with fractional items. | Resource allocation with partial units. | O(n log n) | O(1) | Optimal for fractional items. | Not applicable to 0/1 knapsack. |
| **Huffman Coding** | Builds optimal prefix-free codes for compression. | File compression (e.g., ZIP). | O(n log n) | O(n) | Minimizes code length. | Requires frequency preprocessing. |
| **Job Scheduling** | Optimizes scheduling with deadlines and profits. | Task scheduling in OS. | O(n log n) | O(n) | Maximizes profit. | Specific to deadline-based tasks. |
| **Gas Station Problem** | Determines feasibility of a circular tour. | Route planning for vehicles. | O(n) | O(1) | Linear-time solution. | Assumes fixed gas stations. |
| **Meeting Rooms** | Schedules maximum meetings in fixed rooms. | Conference room allocation. | O(n log n) | O(1) | Efficient interval scheduling. | Limited to single-room variants. |
| **Minimum Platforms** | Minimizes platforms needed for train schedules. | Railway station management. | O(n log n) | O(1) | Optimal resource use. | Specific to time-based scheduling. |
| **Page Replacement** | Optimizes cache page replacement (e.g., LRU). | Cache management in OS. | O(n) for greedy approx | O(k) (k=cache size) | Improves cache hits. | Not always optimal (e.g., vs. OPT). |

### Advanced Greedy Techniques

| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Matroid Theory** | Mathematical framework for greedy algorithms. | Analyzing greedy correctness. | Varies by problem | Varies | Generalizes greedy applicability. | Abstract and complex. |
| **Exchange Arguments** | Proves optimality by swapping solutions. | Proving activity selection correctness. | N/A (proof technique) | N/A | Validates greedy solutions. | Requires problem-specific proof. |
| **Greedy Choice Property** | Ensures local optimal choices lead to global optimum. | Identifying greedy problems. | N/A (design principle) | N/A | Simplifies algorithm design. | Not all problems qualify. |
| **Approximation Algorithms** | Greedy-based near-optimal solutions. | Vertex cover approximation. | O(E) for some problems | O(V) | Fast near-optimal results. | Suboptimal solutions. |
| **Online Algorithms** | Makes greedy decisions with partial data. | Online job scheduling. | Varies by problem | Varies | Handles streaming data. | Limited by unknown future inputs. |
| **Competitive Analysis** | Evaluates online algorithm performance ratios. | Analyzing paging algorithms. | N/A (analysis technique) | N/A | Quantifies performance. | Theoretical focus. |

## Divide and Conquer

Divide and Conquer (D&C) algorithms break problems into smaller subproblems, solve them independently, and combine results. Below are the *Classical D&C Algorithms* and *Advanced D&C Techniques* with comprehensive details.

### Classical D&C Algorithms

| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Merge Sort** | Divides array, sorts halves, and merges. | External sorting of large datasets. | O(n log n) | O(n) auxiliary | Stable and predictable. | Space overhead for merging. |
| **Quick Sort** | Partitions array and recursively sorts. | In-memory general-purpose sorting. | O(n log n) avg, O(n²) worst | O(log n) stack | Fast average case. | Unstable worst-case performance. |
| **Binary Search** | Searches sorted array by halving search space. | Dictionary lookups. | O(log n) | O(1) iterative | Fast for sorted data. | Requires sorted array. |
| **Maximum Subarray** | Finds subarray with maximum sum (Kadane’s extension). | Stock market profit analysis. | O(n) | O(1) | Linear-time solution. | Limited to contiguous sums. |
| **Closest Pair of Points** | Finds closest pair in 2D plane using D&C. | Geographic proximity in mapping. | O(n log n) | O(n) | Efficient geometric solution. | Limited to 2D points. |
| **Strassen’s Algorithm** | Subcubic matrix multiplication via D&C. | Large matrix computations in ML. | O(n^2.81) | O(n²) | Faster than standard multiplication. | High constant factors. |
| **Fast Fourier Transform (FFT)** | Computes discrete Fourier transform efficiently. | Signal processing in audio. | O(n log n) | O(n) | Critical for signal analysis. | Complex implementation. |
| **Karatsuba Multiplication** | Multiplies large integers using D&C. | Cryptographic large-number arithmetic. | O(n^1.585) | O(n) | Faster for large integers. | Overhead for small numbers. |

### Advanced D&C Techniques

| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Master Theorem** | Analyzes recurrence relations for D&C algorithms. | Analyzing merge sort complexity. | N/A (analysis tool) | N/A | Simplifies complexity analysis. | Limited to specific forms. |
| **Akra-Bazzi Theorem** | Generalizes recurrence analysis for D&C. | Complex D&C algorithm analysis. | N/A (analysis tool) | N/A | Handles broader recurrences. | Mathematical complexity. |
| **Decrease and Conquer** | Reduces problem size by a fixed amount. | Binary search variants. | Varies (e.g., O(log n)) | Varies | Simplifies some problems. | Less general than D&C. |
| **Binary Search Variations** | Applies binary search to answers or functions. | Finding square root approximation. | O(log n) | O(1) | Versatile optimization. | Requires monotonicity. |
| **Parallel Divide and Conquer** | Leverages multi-core for D&C tasks. | Parallel merge sort in big data. | O(n/p + log n) (p=cores) | O(n) | Scalable performance. | Parallelization overhead. |
| **Cache-Oblivious Algorithms** | Optimizes D&C for cache performance. | Matrix multiplication in CPUs. | O(n log n) optimal | O(n) | Cache efficiency. | Complex design. |

---

### Backtracking Algorithms

| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **N-Queens Problem** | Places N queens on an NxN chessboard with no conflicts. | Constraint satisfaction testing. | O(n!) | O(n) stack | Solves complex constraints. | Exponential time for large n. |
| **Sudoku Solver** | Fills a 9x9 grid satisfying Sudoku rules. | Puzzle game solvers. | O(9^(n²)) worst case | O(n²) stack | Solves logic puzzles. | Slow for large grids. |
| **Graph Coloring** | Assigns colors to vertices with no adjacent conflicts. | Scheduling with conflict avoidance. | O(k^V) (k=colors, V=vertices) | O(V) stack | Flexible for graph problems. | Exponential complexity. |
| **Hamiltonian Path** | Finds a path visiting all vertices exactly once. | Route planning in networks. | O(n!) | O(n) stack | Solves path problems. | Infeasible for large graphs. |
| **Subset Sum** | Finds subsets summing to a target value. | Budget allocation problems. | O(2^n) | O(n) stack | Exact subset solutions. | Exponential time. |
| **Permutation Generation** | Generates all possible arrangements of a set. | Generating test cases. | O(n!) | O(n) stack | Exhaustive enumeration. | Factorial complexity. |
| **Combination Generation** | Generates all possible selections of k items. | Combinatorial testing. | O(n choose k) | O(k) stack | Efficient for small k. | Large output size. |
| **Maze Solving** | Finds a path through a maze with obstacles. | Robot pathfinding. | O(2^(n*m)) worst case | O(n*m) stack | Solves grid-based paths. | Slow for large mazes. |
| **Word Search** | Finds a word in a grid by exploring paths. | Crossword puzzle solvers. | O(n*m*4^w) (w=word length) | O(w) stack | Flexible string search. | High branching factor. |
| **Expression Evaluation** | Places parentheses for optimal expression evaluation. | Arithmetic expression optimization. | O(2^n) | O(n) stack | Finds optimal solutions. | Exponential complexity. |

### Optimization Techniques

| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Pruning Strategies** | Early termination of unpromising branches. | Reducing search in N-Queens. | Varies, reduces from O(n!) | O(1) auxiliary | Speeds up backtracking. | Problem-specific design. |
| **Constraint Propagation** | Uses forward checking to reduce search space. | Sudoku solver optimization. | Varies, reduces from O(9^(n²)) | O(n²) | Reduces invalid paths. | Overhead in constraint checks. |
| **Heuristic Ordering** | Orders variables/values to prioritize promising choices. | Graph coloring optimization. | Varies, reduces from O(k^V) | O(1) auxiliary | Faster convergence. | Heuristic design complexity. |
| **Backjumping** | Jumps back to the source of conflict in backtracking. | Constraint satisfaction problems. | Varies, reduces from O(n!) | O(n) stack | Avoids redundant exploration. | Complex conflict tracking. |
| **Branch and Bound** | Uses bounds to prune suboptimal solutions. | Traveling Salesman Problem. | Varies, e.g., O(n!) for TSP | O(n) stack | Optimal for optimization problems. | Can still be exponential. |
| **Alpha-Beta Pruning** | Prunes game tree branches in minimax search. | Chess AI move evaluation. | O(b^(d/2)) best (b=branching, d=depth) | O(d) stack | Efficient for game trees. | Limited to adversarial search. |
| **Memoization in Backtracking** | Caches results to avoid recomputation. | Subset sum with repeated calls. | Varies, reduces from O(2^n) | O(n * S) (S=sum) | Avoids redundant work. | Memory overhead. |

---
### Pattern Matching Algorithms

| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Naive String Matching** | Brute-force comparison of pattern with text substrings. | Small-scale text search. | O(n * m) (n=text length, m=pattern length) | O(1) | Simple implementation. | Highly inefficient. |
| **KMP (Knuth-Morris-Pratt)** | Uses prefix table to skip redundant checks. | Text editor search feature. | O(n + m) | O(m) | Linear-time matching. | Preprocessing overhead. |
| **Boyer-Moore** | Skips text using bad character and good suffix heuristics. | Searching large documents. | O(n/m) best, O(n * m) worst | O(k) (k=alphabet size) | Fast for large texts. | Complex preprocessing. |
| **Rabin-Karp** | Uses rolling hash for efficient pattern matching. | Plagiarism detection. | O(n + m) avg, O(n * m) worst | O(1) | Supports multiple patterns. | Hash collision risk. |
| **Z Algorithm** | Computes Z-values for linear-time pattern matching. | String preprocessing for search. | O(n + m) | O(n + m) | Linear-time preprocessing. | Space overhead. |
| **Aho-Corasick** | Automaton for matching multiple patterns simultaneously. | Virus signature scanning. | O(n + m + z) (z=matches) | O(m * k) | Efficient multi-pattern search. | High memory usage. |
| **Shift-And Algorithm** | Uses bitwise operations for pattern matching. | Real-time string matching. | O(n * m / w) (w=word size) | O(m) | Fast with bit operations. | Limited by word size. |

### String Data Structures

| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Suffix Array** | Sorted array of all suffixes of a string. | Full-text search in documents. | O(n log n) build, O(log n) search | O(n) | Versatile string queries. | High build cost. |
| **Suffix Tree** | Compressed trie of all suffixes for pattern matching. | DNA sequence analysis. | O(n) build, O(m) search | O(n) | Fast pattern matching. | High space complexity. |
| **Suffix Automaton** | Recognizes all substrings of a string. | String pattern recognition. | O(n) build, O(m) query | O(n) | Recognizes all substrings. | Complex construction. |
| **Lyndon Words** | Lexicographically minimal rotations of a string. | String factorization in compression. | O(n) | O(n) | Unique string decomposition. | Limited practical use. |
| **Burrows-Wheeler Transform** | Reorders string for compression preprocessing. | BZIP2 compression algorithm. | O(n) | O(n) | Enhances compression. | Requires inverse transform. |
| **FM-Index** | Full-text index based on BWT for efficient search. | Genomic sequence search. | O(n) build, O(m) search | O(n) | Space-efficient search. | Complex implementation. |
| **Wavelet Tree** | Tree for range queries on strings or sequences. | Compressed text range queries. | O(n log σ) build, O(log σ) query | O(n log σ) (σ=alphabet size) | Efficient range queries. | Alphabet size dependency. |
| **Compressed Suffix Arrays** | Space-efficient suffix array representation. | Memory-constrained text indexing. | O(n log n) build, O(log n) query | O(n / log n) | Saves space. | Slower queries than suffix arrays. |

### Advanced String Problems

| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Longest Common Substring** | Finds longest substring common to two strings. | Plagiarism detection in texts. | O(n * m) DP | O(n * m) | Exact substring matching. | Space-intensive. |
| **Longest Palindromic Substring** | Finds longest palindromic substring (Manacher’s). | DNA palindrome detection. | O(n) | O(n) | Linear-time palindrome search. | Limited to palindromes. |
| **String Hashing** | Uses polynomial rolling hash for string comparison. | Substring equality checks. | O(n) preprocess, O(1) compare | O(n) | Fast substring comparisons. | Hash collision risk. |
| **Edit Distance Variants** | Computes string transformation metrics (e.g., Levenshtein). | Spell correction in editors. | O(n * m) | O(n * m) | Flexible string metrics. | High time/space complexity. |
| **Approximate String Matching** | Finds patterns with allowed errors (fuzzy matching). | Search with typos in queries. | O(n * m) DP | O(n * m) | Handles errors in matching. | Computationally expensive. |
| **String Compression** | Compresses strings using LZ77, LZ78, or LZW. | File compression (e.g., ZIP). | O(n) | O(n) | Reduces storage size. | Decompression overhead. |
| **Regular Expression Matching** | Matches strings using NFA/DFA construction. | Pattern matching in text editors. | O(n * m) | O(m) | Flexible pattern matching. | Complex regex parsing. |
| **Palindrome Tree (Eertree)** | Data structure for all palindromic substrings. | Palindrome analysis in strings. | O(n) build | O(n) | Efficient palindrome queries. | Specialized use case. |

---
### Number Theory

| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **GCD and LCM** | Computes greatest common divisor and least common multiple using Euclidean algorithm. | Simplifying fractions. | O(log min(a, b)) | O(1) | Fast and simple. | Limited to positive integers. |
| **Extended Euclidean Algorithm** | Finds Bézout coefficients for GCD. | Solving linear Diophantine equations. | O(log min(a, b)) | O(1) | Computes modular inverses. | Complex for non-GCD tasks. |
| **Modular Arithmetic** | Performs addition, multiplication, and exponentiation under modulo. | Cryptographic computations. | O(1) for basic ops | O(1) | Efficient for large numbers. | Overflow without proper modulo. |
| **Fast Exponentiation** | Computes large powers using binary exponentiation. | RSA key generation. | O(log n) | O(1) | Fast for large exponents. | Limited to exponentiation. |
| **Modular Inverse** | Finds multiplicative inverse using extended Euclidean algorithm. | Modular division in cryptography. | O(log n) | O(1) | Enables division in modular systems. | Exists only if coprime. |
| **Chinese Remainder Theorem** | Solves system of modular congruences. | Reconstructing numbers in cryptography. | O(k log m) (k=moduli, m=product) | O(k) | Solves multiple congruences. | Requires coprime moduli. |
| **Prime Generation** | Generates primes using Sieve of Eratosthenes variants. | Cryptographic key setup. | O(n log log n) | O(n) | Efficient for large ranges. | Memory-intensive for large n. |
| **Prime Testing** | Tests primality using Miller-Rabin or Solovay-Strassen. | Primality checks in RSA. | O(k log³ n) (k=iterations) | O(1) | Fast probabilistic testing. | Small error probability. |
| **Integer Factorization** | Factors integers using Pollard’s rho or quadratic sieve. | Breaking RSA encryption. | O(√n) Pollard, subexp quadratic sieve | O(log n) | Breaks down large numbers. | Slow for very large numbers. |

### Combinatorics

| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Permutations and Combinations** | Counts arrangements and selections of items. | Password generation analysis. | O(n!) perms, O(n choose k) | O(1) | Fundamental counting tool. | Factorial growth for perms. |
| **Catalan Numbers** | Counts structures like balanced parentheses or binary trees. | Counting valid parentheses. | O(n) with DP | O(n) | Versatile combinatorial counts. | Limited to specific structures. |
| **Stirling Numbers** | Counts set partitions (first/second kind). | Clustering analysis. | O(n * k) with DP | O(n * k) | Counts partition structures. | Complex recurrence. |
| **Bell Numbers** | Counts total partitions of a set. | Partitioning objects in groups. | O(n²) with DP | O(n) | Simple partition counting. | Quadratic complexity. |
| **Fibonacci Numbers** | Sequence defined by recurrence relations. | Algorithm complexity analysis. | O(n) with DP | O(1) optimized | Simple recurrence model. | Limited practical use. |
| **Lucas Numbers** | Fibonacci-like sequence with different initial conditions. | Number theory problems. | O(n) with DP | O(1) optimized | Similar to Fibonacci. | Niche applications. |
| **Binomial Coefficients** | Computes combinations using Pascal’s triangle. | Probability calculations. | O(n * k) with DP | O(n * k) | Efficient combination counts. | Large values need modulo. |
| **Inclusion-Exclusion Principle** | Counts elements with overlapping properties. | Counting derangements. | O(2^n) | O(1) | Handles overlapping sets. | Exponential for many sets. |
| **Generating Functions** | Solves combinatorial problems using series. | Counting coin change ways. | O(n log n) with FFT | O(n) | Powerful for recurrences. | Mathematical complexity. |
| **Burnside’s Lemma** | Counts distinct objects under group actions. | Counting distinct necklaces. | O(n * |G|) (|G|=group size) | O(n) | Handles symmetry. | Requires group theory knowledge. |

### Geometry

| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Convex Hull** | Finds smallest convex polygon enclosing points (Graham scan, Jarvis march, QuickHull). | Collision detection in games. | O(n log n) Graham, O(nh) Jarvis | O(n) | Efficient boundary computation. | Limited to 2D/3D points. |
| **Line Intersection** | Determines if and where two line segments intersect. | CAD software design. | O(1) per pair | O(1) | Fast intersection checks. | Precision issues in floating-point. |
| **Point in Polygon** | Checks if a point lies inside a polygon (ray casting, winding number). | Geographic information systems. | O(n) | O(1) | Simple containment test. | Slow for complex polygons. |
| **Closest Pair of Points** | Finds closest pair of points in a plane using D&C. | Proximity analysis in maps. | O(n log n) | O(n) | Efficient geometric search. | Limited to 2D points. |
| **Voronoi Diagrams** | Partitions plane based on nearest points. | Nearest facility location. | O(n log n) | O(n) | Useful for spatial analysis. | Complex construction. |
| **Delaunay Triangulation** | Creates triangulation maximizing minimum angles. | Mesh generation in graphics. | O(n log n) | O(n) | Avoids skinny triangles. | Computationally intensive. |
| **Sweep Line Algorithms** | Processes geometric events using a sweep line. | Line segment intersection detection. | O((n + k) log n) (k=intersections) | O(n) | Efficient event handling. | Problem-specific design. |
| **Rotating Calipers** | Computes diameter or width of a convex polygon. | Shape analysis in robotics. | O(n) after hull | O(n) | Fast after convex hull. | Requires convex hull first. |

---
### Approximation Algorithms

| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Vertex Cover** | 2-approximation algorithm for minimum vertex cover. | Network monitoring node selection. | O(V + E) | O(V) | Guaranteed 2-approximation. | Not optimal for small graphs. |
| **Set Cover** | Greedy algorithm with logarithmic approximation. | Facility coverage planning. | O(n log n) (n=elements) | O(n) | Logarithmic approximation. | Suboptimal for large sets. |
| **Traveling Salesman** | Christofides algorithm for metric TSP (1.5-approximation). | Delivery route optimization. | O(n³) | O(n²) | 1.5-approximation for metric TSP. | Limited to metric spaces. |
| **Bin Packing** | First fit, best fit heuristics for bin packing. | Resource allocation in cloud. | O(n log n) | O(n) | Fast heuristic solution. | Not guaranteed optimal. |
| **Load Balancing** | List scheduling for task assignment. | Task distribution in clusters. | O(n log m) (m=machines) | O(n) | Simple and effective. | Can be far from optimal. |
| **Facility Location** | Primal-dual approximation for facility placement. | Warehouse location planning. | O(n²) | O(n) | Balanced cost approximation. | Complex dual formulation. |
| **Steiner Tree** | MST-based approximation for Steiner tree problem. | Network design with extra nodes. | O(n log n) | O(n) | Simple MST-based approach. | Suboptimal for non-MST cases. |

### Randomized Algorithms

| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Las Vegas Algorithms** | Always correct with random runtime (e.g., randomized quicksort). | Sorting large datasets. | O(n log n) expected | O(log n) | Guaranteed correctness. | Variable runtime. |
| **Monte Carlo Algorithms** | Probabilistic correctness with fixed runtime. | Primality testing (Miller-Rabin). | O(k log³ n) (k=iterations) | O(1) | Fast with high probability. | Small error probability. |
| **Randomized QuickSort** | Random pivot selection for expected O(n log n). | General-purpose sorting. | O(n log n) expected | O(log n) stack | Avoids worst-case O(n²). | Randomness dependency. |
| **Skip Lists** | Probabilistic balanced data structure for search. | In-memory key-value stores. | O(log n) expected | O(n) | Simple balanced structure. | Probabilistic performance. |
| **Randomized Selection** | Finds k-th smallest element in linear expected time. | Median finding in arrays. | O(n) expected | O(1) | Linear expected time. | Variable runtime. |
| **Bloom Filters** | Probabilistic set membership with false positives. | Cache filtering in databases. | O(1) insert/query | O(m) bits | Space-efficient. | False positives. |
| **Hash Function Construction** | Universal hashing to minimize collisions. | Hash table optimization. | O(1) expected | O(1) | Collision resistance. | Setup overhead. |
| **Reservoir Sampling** | Randomly samples k items from a stream. | Streaming data analysis. | O(n) | O(k) | Handles unknown stream size. | Fixed sample size. |

### Online Algorithms

| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Competitive Analysis** | Evaluates worst-case performance ratios for online algorithms. | Analyzing paging algorithms. | N/A (analysis technique) | N/A | Quantifies online performance. | Theoretical focus. |
| **Paging Algorithms** | Manages cache pages (e.g., LRU, FIFO). | OS memory management. | O(1) per request | O(k) (k=cache size) | Practical cache management. | Suboptimal vs. offline OPT. |
| **Load Balancing** | Distributes tasks online across machines. | Server task allocation. | O(log m) per task (m=machines) | O(m) | Dynamic load distribution. | Can be unbalanced. |
| **Ski Rental Problem** | Decides buy vs. rent with partial information. | Resource leasing decisions. | O(1) per decision | O(1) | Simple decision rule. | Limited to buy/rent model. |
| **Online Matching** | Matches arriving nodes in bipartite graphs. | Ad allocation in auctions. | O(E) | O(V) | Handles real-time arrivals. | Suboptimal vs. offline. |
| **Secretary Problem** | Selects best candidate with optimal stopping. | Hiring best candidate online. | O(n) | O(1) | Optimal stopping strategy. | Limited to single selection. |
| **Caching Strategies** | Manages online cache with eviction policies. | Web browser caching. | O(1) per access | O(k) | Improves access speed. | Suboptimal eviction choices. |

### Parallel Algorithms

| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **PRAM Models** | Parallel Random Access Machine for theoretical parallel algorithms. | Analyzing parallel complexity. | Varies (e.g., O(log n)) | Varies | Theoretical parallel framework. | Unrealistic memory model. |
| **Work and Span** | Measures parallel work (total ops) and span (critical path). | Evaluating parallel algorithms. | N/A (analysis metrics) | N/A | Quantifies parallel efficiency. | Theoretical focus. |
| **Parallel Prefix (Scan)** | Computes prefix sums in parallel. | Stream compaction in GPUs. | O(log n) span | O(n) | Fast parallel sums. | Requires parallel hardware. |
| **Parallel Merge** | Merges sorted sequences in parallel. | Parallel merge sort. | O(log n) span | O(n) | Scalable merging. | Synchronization overhead. |
| **Parallel Matrix Multiplication** | Distributes matrix multiplication across processors. | Large-scale ML computations. | O(log n) span | O(n²) | High parallel speedup. | Communication overhead. |
| **Parallel Graph Algorithms** | Parallel BFS or connected components. | Social network analysis. | O(log n) span for BFS | O(V + E) | Scalable graph processing. | Complex synchronization. |
| **Fork-Join Model** | Divides tasks into subtasks for parallel execution. | Multithreaded task scheduling. | O(log n) span | O(n) | Simple parallel framework. | Overhead in task division. |
| **Work-Stealing** | Dynamically balances load in parallel tasks. | Parallel task frameworks (e.g., Cilk). | O(log n) span | O(n) | Efficient load balancing. | Runtime overhead. |

---
### Memory Management

| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Garbage Collection** | Reclaims unused memory (e.g., mark-and-sweep, generational GC). | Java runtime memory management. | O(n) mark-and-sweep | O(n) | Automates memory cleanup. | Pauses application execution. |
| **Memory Allocation** | Allocates memory blocks (e.g., buddy system, slab allocation). | Kernel memory allocation. | O(log n) buddy, O(1) slab | O(n) | Efficient block allocation. | Fragmentation issues. |
| **Cache Replacement** | Evicts cache items (e.g., LRU, LFU, ARC). | CPU cache management. | O(1) LRU with hash | O(n) | Improves cache hit rates. | Suboptimal vs. offline OPT. |
| **Page Replacement** | Replaces virtual memory pages (e.g., FIFO, optimal, working set). | OS virtual memory handling. | O(1) FIFO | O(n) | Minimizes page faults. | Optimal is impractical. |
| **Virtual Memory** | Manages memory via paging or segmentation. | Process memory isolation in OS. | O(1) page table lookup | O(n) | Enables large address spaces. | TLB miss overhead. |
| **Memory Compaction** | Relocates memory to reduce fragmentation. | Defragmenting heap in OS. | O(n) | O(1) auxiliary | Reduces fragmentation. | High runtime overhead. |
| **Reference Counting** | Tracks object references for memory reclamation. | Python memory management. | O(1) per operation | O(n) | Immediate reclamation. | Cyclic reference issues. |
| **Copy Collection** | Stop-and-copy garbage collection by copying live objects. | Real-time GC in embedded systems. | O(n) live objects | O(n/2) | Eliminates fragmentation. | Requires double space. |

### I/O and Storage

| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Disk Scheduling** | Optimizes disk head movement (e.g., FCFS, SSTF, SCAN, C-SCAN). | Hard drive request handling. | O(n) SSTF | O(n) queue | Minimizes seek time. | Starvation in SSTF. |
| **File System Operations** | Manages file storage (e.g., FAT, NTFS, ext4 structures). | File access in OS. | O(log n) ext4 lookup | O(n) | Efficient file organization. | Complexity varies by system. |
| **B+ Tree Indexing** | Uses B+ trees for efficient database storage. | Database query optimization. | O(log n) search | O(n) | Fast range queries. | Space overhead. |
| **Log-Structured Systems** | Uses append-only storage for high write throughput. | SSD file systems (e.g., F2FS). | O(1) write | O(n) | High write performance. | Garbage collection overhead. |
| **Copy-on-Write** | Duplicates data only when modified. | File system snapshots (e.g., ZFS). | O(1) copy | O(n) | Efficient snapshots. | Space usage for updates. |
| **Wear Leveling** | Distributes writes to extend SSD lifetime. | SSD firmware management. | O(1) per write | O(n) | Prolongs SSD lifespan. | Controller complexity. |
| **Deduplication** | Eliminates duplicate data blocks. | Backup storage optimization. | O(n log n) hash-based | O(n) | Saves storage space. | Hash collision risk. |
| **Compression** | Reduces data size using LZ77, LZ78, or deflate. | File compression (e.g., ZIP). | O(n) compression | O(n) | Reduces storage/transfer size. | Decompression overhead. |

### Network Algorithms

| Type | Description | Example Use Case | Time Complexity | Space Complexity | Key Advantage | Key Limitation |
|------|-------------|------------------|-----------------|------------------|---------------|----------------|
| **Routing Algorithms** | Determines paths in networks (e.g., distance vector, link state). | Internet routing (e.g., OSPF). | O(V²) Bellman-Ford | O(V) | Efficient path selection. | Convergence delays. |
| **Congestion Control** | Manages network traffic (e.g., TCP congestion algorithms). | TCP data transmission. | O(1) per packet | O(1) | Prevents network overload. | Slow adaptation to changes. |
| **Load Balancing** | Distributes network traffic (e.g., round-robin, least connections). | Web server traffic distribution. | O(1) round-robin | O(n) | Even resource usage. | Suboptimal for dynamic loads. |
| **Rate Limiting** | Controls request rates (e.g., token bucket, leaky bucket). | API request throttling. | O(1) per request | O(1) | Prevents system overload. | Parameter tuning complexity. |
| **Network Flow** | Applies max flow algorithms to network problems. | Bandwidth allocation. | O(V * E²) Edmonds-Karp | O(V + E) | Optimizes resource flow. | High computational cost. |
| **Spanning Tree Protocol** | Prevents loops in Ethernet networks. | LAN switch configuration. | O(V + E) | O(V) | Ensures loop-free topology. | Slow convergence. |
| **Multicast Routing** | Uses Steiner tree for efficient multicast. | Video streaming distribution. | O(n log n) approx | O(n) | Minimizes bandwidth usage. | NP-hard exact solution. |
| **Quality of Service** | Shapes traffic for prioritized delivery. | VoIP traffic prioritization. | O(n) per packet | O(n) | Ensures service reliability. | Complex policy management. |

---
