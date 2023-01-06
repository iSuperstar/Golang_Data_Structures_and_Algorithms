# Simple Array
```go
// Create an array of integers with a length of 5.
// The array is initialized with the default value for the element type (0 for integers).
var arr [5]int

// Set the value of the first element in the array.
arr[0] = 1

// Get the value of the second element in the array.
x := arr[1]

// Iterate over the elements in the array.
for i, value := range arr {
    fmt.Printf("Index: %d, Value: %d\n", i, value)
}

// Create an array of strings with a length of 3 and initialized with values.
words := [3]string{"apple", "banana", "cherry"}

// Get the length of the array.
length := len(words)

// Check if the array is empty.
isEmpty := len(words) == 0
```

# Multi-dimensional Array
```go
// Create a 2x3 array of integers.
// The array is initialized with the default value for the element type (0 for integers).
var arr [2][3]int

// Set the value of the element at row 0, column 1.
arr[0][1] = 1

// Get the value of the element at row 1, column 2.
x := arr[1][2]

// Iterate over the elements in the array.
for i, row := range arr {
    for j, value := range row {
        fmt.Printf("Row: %d, Column: %d, Value: %d\n", i, j, value)
    }
}

// Create a 3x3 array of strings and initialize it with values.
words := [3][3]string{
    {"red", "green", "blue"},
    {"apple", "banana", "cherry"},
    {"dog", "cat", "bird"},
}

// Get the number of rows in the array.
numRows := len(words)

// Get the number of columns in the array.
numColumns := len(words[0])

// Check if the array is empty.
isEmpty := len(words) == 0
```

# Associative Array
```go
// Create a map that maps strings to integers.
// The map is initialized as empty.
var m map[string]int

// Set the value for the key "apple".
m["apple"] = 1

// Get the value for the key "banana".
x := m["banana"]

// Check if the key "cherry" is in the map.
_, ok := m["cherry"]

// Iterate over the key-value pairs in the map.
for key, value := range m {
    fmt.Printf("Key: %s, Value: %d\n", key, value)
}

// Create a map that maps strings to strings and initialize it with values.
colors := map[string]string{
    "red":   "#ff0000",
    "green": "#00ff00",
    "blue":  "#0000ff",
}

// Get the number of key-value pairs in the map.
numEntries := len(colors)

// Check if the map is empty.
isEmpty := len(colors) == 0

// Delete a key-value pair from the map.
delete(colors, "red")
```
# Simple Weighted Graph
```go
package main

import "fmt"

// Edge represents an edge in the graph with a weight.
type Edge struct {
        To int
        Weight int
}

// WeightedGraph represents a graph where each edge has a weight.
type WeightedGraph struct {
        Edges []map[int][]Edge
        NumVertices int
}

// AddEdge adds an edge to the graph with the given weight.
func (g *WeightedGraph) AddEdge(from, to, weight int) {
        g.Edges[from][to] = append(g.Edges[from][to], Edge{To: to, Weight: weight})
}

// GetEdges returns all the edges for the given vertex.
func (g *WeightedGraph) GetEdges(vertex int) []Edge {
        edges := []Edge{}
        for to, edgeList := range g.Edges[vertex] {
                for _, edge := range edgeList {
                        if edge.To == to {
                                edges = append(edges, edge)
                        }
                }
        }
        return edges
}

func main() {
        g := WeightedGraph{NumVertices: 3, Edges: make([]map[int][]Edge, 3)}
        for i := range g.Edges {
                g.Edges[i] = make(map[int][]Edge)
        }
        g.AddEdge(0, 1, 10)
        g.AddEdge(1, 2, 20)
        g.AddEdge(2, 0, 30)

        fmt.Println(g.GetEdges(1))
}
```

# Simple Unweighted Graph
```go
package main

import "fmt"

// Graph represents an unweighted graph.
type Graph struct {
        Edges []map[int]bool
        NumVertices int
}

// AddEdge adds an edge to the graph.
func (g *Graph) AddEdge(from, to int) {
        g.Edges[from][to] = true
}

// HasEdge returns true if there is an edge between the given vertices.
func (g *Graph) HasEdge(from, to int) bool {
        _, ok := g.Edges[from][to]
        return ok
}

func main() {
        g := Graph{NumVertices: 3, Edges: make([]map[int]bool, 3)}
        for i := range g.Edges {
                g.Edges[i] = make(map[int]bool)
        }
        g.AddEdge(0, 1)
        g.AddEdge(1, 2)
        g.AddEdge(2, 0)

        fmt.Println(g.HasEdge(1, 2))
        fmt.Println(g.HasEdge(2, 1))
}
```

# Simple Directed Graph
```go
package main

import "fmt"

// Graph represents a directed graph.
type Graph struct {
        Edges map[int]map[int]bool
        NumVertices int
}

// AddEdge adds an edge to the graph.
func (g *Graph) AddEdge(from, to int) {
        if g.Edges[from] == nil {
                g.Edges[from] = make(map[int]bool)
        }
        g.Edges[from][to] = true
}

// HasEdge returns true if there is an edge between the given vertices.
func (g *Graph) HasEdge(from, to int) bool {
        _, ok := g.Edges[from][to]
        return ok
}

func main() {
        g := Graph{NumVertices: 3, Edges: make(map[int]map[int]bool)}
        g.AddEdge(0, 1)
        g.AddEdge(1, 2)
        g.AddEdge(2, 0)

        fmt.Println(g.HasEdge(1, 2))
        fmt.Println(g.HasEdge(2, 1))
}
```

# Simple Undirected Graph
```go
package main

import "fmt"

// Graph represents an undirected graph.
type Graph struct {
        Edges map[int]map[int]bool
        NumVertices int
}

// AddEdge adds an edge to the graph.
func (g *Graph) AddEdge(from, to int) {
        if g.Edges[from] == nil {
                g.Edges[from] = make(map[int]bool)
        }
        if g.Edges[to] == nil {
                g.Edges[to] = make(map[int]bool)
        }
        g.Edges[from][to] = true
        g.Edges[to][from] = true
}

// HasEdge returns true if there is an edge between the given vertices.
func (g *Graph) HasEdge(from, to int) bool {
        _, ok := g.Edges[from][to]
        return ok
}

func main() {
        g := Graph{NumVertices: 3, Edges: make(map[int]map[int]bool)}
        g.AddEdge(0, 1)
        g.AddEdge(1, 2)
        g.AddEdge(2, 0)

        fmt.Println(g.HasEdge(1, 2))
        fmt.Println(g.HasEdge(2, 1))
}
```
# Single LinkedList in Go
```go
type Node struct {
    Value int
    Next *Node
}

type LinkedList struct {
    Head *Node
}

func (l *LinkedList) InsertAfter(node *Node, value int) {
    newNode := &Node{Value: value}
    newNode.Next = node.Next
    node.Next = newNode
}

func (l *LinkedList) Append(value int) {
    newNode := &Node{Value: value}

    if l.Head == nil {
        l.Head = newNode
        return
    }

    currentNode := l.Head
    for currentNode.Next != nil {
        currentNode = currentNode.Next
    }
    currentNode.Next = newNode
}

func (l *LinkedList) Prepend(value int) {
    newNode := &Node{Value: value}
    newNode.Next = l.Head
    l.Head = newNode
}

func (l *LinkedList) Delete(value int) {
    if l.Head == nil {
        return
    }

    if l.Head.Value == value {
        l.Head = l.Head.Next
        return
    }

    currentNode := l.Head
    for currentNode.Next != nil {
        if currentNode.Next.Value == value {
            currentNode.Next = currentNode.Next.Next
            return
        }
        currentNode = currentNode.Next
    }
}
```

# Circular LinkedList in Go
```go
type Node struct {
    Value int
    Next *Node
}

type CircularLinkedList struct {
    Head *Node
}

func (c *CircularLinkedList) InsertAfter(node *Node, value int) {
    newNode := &Node{Value: value}
    newNode.Next = node.Next
    node.Next = newNode
}

func (c *CircularLinkedList) Append(value int) {
    newNode := &Node{Value: value}

    if c.Head == nil {
        c.Head = newNode
        newNode.Next = c.Head
        return
    }

    currentNode := c.Head
    for currentNode.Next != c.Head {
        currentNode = currentNode.Next
    }
    currentNode.Next = newNode
    newNode.Next = c.Head
}

func (c *CircularLinkedList) Prepend(value int) {
    newNode := &Node{Value: value}
    newNode.Next = c.Head
    currentNode := c.Head

    if c.Head == nil {
        c.Head = newNode
        newNode.Next = c.Head
        return
    }

    for currentNode.Next != c.Head {
        currentNode = currentNode.Next
    }
    currentNode.Next = newNode
    c.Head = newNode
}

func (c *CircularLinkedList) Delete(value int) {
    if c.Head == nil {
        return
    }

    if c.Head.Value == value {
        currentcurrentNode := c.Head
    for currentNode.Next != c.Head {
        if currentNode.Next.Value == value {
            currentNode.Next = currentNode.Next.Next
            return
        }
        currentNode = currentNode.Next
    }

    if currentNode.Value == value {
        currentNode.Next = currentNode.Next.Next
        c.Head = currentNode.Next
    }
}
```

# Doubly LinkedList
```go
type Node struct {
    Value int
    Prev *Node
    Next *Node
}

type DoublyLinkedList struct {
    Head *Node
    Tail *Node
}

func (d *DoublyLinkedList) InsertAfter(node *Node, value int) {
    newNode := &Node{Value: value}
    newNode.Prev = node
    newNode.Next = node.Next
    node.Next = newNode
}

func (d *DoublyLinkedList) Append(value int) {
    newNode := &Node{Value: value}

    if d.Head == nil {
        d.Head = newNode
        d.Tail = newNode
        return
    }

    d.Tail.Next = newNode
    newNode.Prev = d.Tail
    d.Tail = newNode
}

func (d *DoublyLinkedList) Prepend(value int) {
    newNode := &Node{Value: value}

    if d.Head == nil {
        d.Head = newNode
        d.Tail = newNode
        return
    }

    d.Head.Prev = newNode
    newNode.Next = d.Head
    d.Head = newNode
}

func (d *DoublyLinkedList) Delete(value int) {
    currentNode := d.Head
    for currentNode != nil {
        if currentNode.Value == value {
            currentNode.Prev.Next = currentNode.Next
            currentNode.Next.Prev = currentNode.Prev
            return
        }
        currentNode = currentNode.Next
    }
}
```
# Simple Queue Data Structure
```go
type Queue struct {
    items []int
}

func (q *Queue) Enqueue(item int) {
    q.items = append(q.items, item)
}

func (q *Queue) Dequeue() int {
    item := q.items[0]
    q.items = q.items[1:]
    return item
}

func (q *Queue) IsEmpty() bool {
    return len(q.items) == 0
}

func (q *Queue) Size() int {
    return len(q.items)
}
```

# Circular Queue
```go
type CircularQueue struct {
    items []int
    head int
    tail int
    size int
}

func (cq *CircularQueue) Enqueue(item int) {
    if cq.size == len(cq.items) {
        cq.resize()
    }
    cq.items[cq.tail] = item
    cq.tail = (cq.tail + 1) % len(cq.items)
    cq.size++
}

func (cq *CircularQueue) Dequeue() int {
    if cq.IsEmpty() {
        panic("Cannot dequeue from an empty queue")
    }
    item := cq.items[cq.head]
    cq.head = (cq.head + 1) % len(cq.items)
    cq.size--
    return item
}

func (cq *CircularQueue) IsEmpty() bool {
    return cq.size == 0
}

func (cq *CircularQueue) Size() int {
    return cq.size
}

func (cq *CircularQueue) resize() {
    newItems := make([]int, 2*len(cq.items))
    for i := 0; i < cq.size; i++ {
        newItems[i] = cq.items[(cq.head+i)%len(cq.items)]
    }
    cq.items = newItems
    cq.head = 0
    cq.tail = cq.size
}
```

# Priority Queue
```go
type Item struct {
    value    interface{}
    priority int
    index    int
}

type PriorityQueue []*Item

func (pq PriorityQueue) Len() int { return len(pq) }

func (pq PriorityQueue) Less(i, j int) bool {
    return pq[i].priority < pq[j].priority
}

func (pq PriorityQueue) Swap(i, j int) {
    pq[i], pq[j] = pq[j], pq[i]
    pq[i].index = i
    pq[j].index = j
}

func (pq *PriorityQueue) Push(x interface{}) {
    n := len(*pq)
    item := x.(*Item)
    item.index = n
    *pq = append(*pq, item)
}

func (pq *PriorityQueue) Pop() interface{} {
    old := *pq
    n := len(old)
    item := old[n-1]
    item.index = -1 // for safety
    *pq = old[0 : n-1]
    return item
}

// update modifies the priority and value of an Item in the queue.
func (pq *PriorityQueue) update(item *Item, value interface{}, priority int) {
    item.value = value
    item.priority = priority
    heap.Fix(pq, item.index)
}
```

# Double Ended Queue (deque)
```go
type Deque struct {
    items []int
    head int
    tail int
    size int
}

func (d *Deque) PushFront(item int) {
    if d.size == len(d.items) {
        d.resize()
    }
    d.head = (d.head - 1 + len(d.items)) % len(d.items)
    d.items[d.head] = item
    d.size++
}

func (d *Deque) PushBack(item int) {
    if d.size == len(d.items) {
        d.resize()
    }
    d.items[d.tail] = item
    d.tail = (d.tail + 1) % len(d.items)
    d.size++
}

func (d *Deque) PopFront() int {
    if d.IsEmpty() {
        panic("Cannot pop from an empty deque")
    }
    item := d.items[d.head]
    d.head = (d.head + 1) % len(d.items)
    d.size--
    return item
}

func (d *Deque) PopBack() int {
    if d.IsEmpty() {
        panic("Cannot pop from an empty deque")
    }
    d.tail = (d.tail - 1 + len(d.items)) % len(d.items)
    item := d.items[d.tail]
    d.size--
    return item
}

func (d *Deque) IsEmpty() bool {
    return d.size == 0
}

func (d *Deque) resize() {
    newItems := make([]int, 2*len(d.items))
    for i := 0; i < d.size; i++ {
        newItems[i] = d.items[(d.head+i)%len(d.items)]
    }
    d.items = newItems
    d.head = 0
    d.tail = d.size
}
```
# Simple Stack Data Structure
```go
type Stack struct {
    items []int
}

func (s *Stack) Push(item int) {
    s.items = append(s.items, item)
}

func (s *Stack) Pop() int {
    item := s.items[len(s.items)-1]
    s.items = s.items[:len(s.items)-1]
    return item
}

func (s *Stack) IsEmpty() bool {
    return len(s.items) == 0
}

func (s *Stack) Peek() int {
    return s.items[len(s.items)-1]
}

func (s *Stack) Size() int {
    return len(s.items)
}
```
# Simple Binary Tree
```go
type Node struct {
    Value int
    Left *Node
    Right *Node
}

type BinaryTree struct {
    Root *Node
}

func (b *BinaryTree) Insert(value int) {
    newNode := &Node{Value: value}

    if b.Root == nil {
        b.Root = newNode
        return
    }

    currentNode := b.Root
    for {
        if value < currentNode.Value {
            if currentNode.Left == nil {
                currentNode.Left = newNode
                return
            }
            currentNode = currentNode.Left
        } else {
            if currentNode.Right == nil {
                currentNode.Right = newNode
                return
            }
            currentNode = currentNode.Right
        }
    }
}

func (b *BinaryTree) Search(value int) bool {
    currentNode := b.Root
    for currentNode != nil {
        if value == currentNode.Value {
            return true
        } else if value < currentNode.Value {
            currentNode = currentNode.Left
        } else {
            currentNode = currentNode.Right
        }
    }
    return false
}
```

# Simple Binary Search Tree
```go
type Node struct {
    Value int
    Left *Node
    Right *Node
}

type BinarySearchTree struct {
    Root *Node
}

func (b *BinarySearchTree) Insert(value int) {
    newNode := &Node{Value: value}

    if b.Root == nil {
        b.Root = newNode
        return
    }

    currentNode := b.Root
    for {
        if value < currentNode.Value {
            if currentNode.Left == nil {
                currentNode.Left = newNode
                return
            }
            currentNode = currentNode.Left
        } else {
            if currentNode.Right == nil {
                currentNode.Right = newNode
                return
            }
            currentNode = currentNode.Right
        }
    }
}

func (b *BinarySearchTree) Search(value int) bool {
    currentNode := b.Root
    for currentNode != nil {
        if value == currentNode.Value {
            return true
        } else if value < currentNode.Value {
            currentNode = currentNode.Left
        } else {
            currentNode = currentNode.Right
        }
    }
    return false
}
```
