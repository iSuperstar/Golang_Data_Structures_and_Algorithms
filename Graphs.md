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
