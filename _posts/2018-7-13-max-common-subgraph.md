---
layout: post
title: Maximum common subgraph is NP-complete
category: cpsc420
---

## Set Up
_Input_: Two graphs *G<sub>1</sub>* = (*V<sub>1</sub>*,*E<sub>1</sub>*) and *G<sub>2</sub>* = (*V<sub>2</sub>* , *E<sub>2</sub>*); a budget *b*.<br>
_Output_: Two sets of nodes *V*<sub>1</sub>′ ⊆ *V*<sub>1</sub> and *V*<sub>2</sub>′⊆ *V*<sub>2</sub> whose deletion leaves at least b nodes in each graph, and makes the two graphs identical.
## Proof
(1) Proof that MCS ∈ NP  
Certificate: two set of vertices *V*<sub>1</sub>′, *V*<sub>2</sub>′ of
size *b* after deletions from *G*<sub>1</sub> and *G*<sub>2</sub>  
Verifier: check that the returned set of vertices from both graphs,
*V*<sub>1</sub>′ and *V*<sub>2</sub>′ are identical and each edge in
*G*<sub>1</sub> maps to an edge in *G*<sub>2</sub> and has at least *b*
vertices, this can be done using a for-loop inside a for-loop.  
∴ MCS ∈ NP  
(2) Proof MCS is NP-Complete  
Show : Independent set ≤<sub>*p*</sub> MCS  
Given a graph, *G* = (*V*, *E*) and integer, *k* construct a
complementary graph *G*′ = (*V*′, *E*′) such that *G*′ has all the same
vertices as *G* i.e. *V*′ = *V* and *G*′ has a set of edges *E*′ such
that for all nodes *u*, *v* ∈ *V*, edge *e* = (*u*, *v*) ∈ *E*′ if and
only if *e* ∉ *E*.  
If *G*′ has an independent set of size *k* then that means the set has
edges between them in the original graph *G* and form a complete
subgraph of size *k* in *G*. Let this subgraph of size *k* be denoted by
*G*<sub>1</sub> and let the original graph *G* = *G*<sub>2</sub>.  
Now after |*V*| − *k* vertex deletions in *G*<sub>2</sub> there will be
a graph that contains *V*<sub>2</sub> ⊂ *V* such that *V*<sub>2</sub> is
isomorphic to *V*<sub>1</sub> and contains *k* vertices. This is also a
instance of maximum common subgraph where we know the MCG is the
complete subgraph of size *k*, *G*<sub>1</sub> found using the
complement of *G* and deleting |*V*| − *k* nodes in
*G*<sub>2</sub> = *G* to generate a graph isomorphic to
*G*<sub>1</sub>.  
*Proof of runtime:*  
Copying the vertices to make the complement graph takes *O*(*n*) where
|*V*| = *n*, likewise copying edges to the complementary graph takes at
most linear time in respect to the size of the set of edges.  
*Proof of correctness:*  
⇒ Given an independent set of size *k* is the complementary graph, *G*′
of *G*, implies the same vertices in *G* are connected by edges forming
a subgraph of size *k*, *G*<sub>1</sub>, and by deleting |*V*| − *k*
vertices in the original graph, you can obtain an isomorphic graph to
the complete subgraph of size *k*, this is an instance of MCG.
Therefore, there is an independent set of size *k* in *G*′ if there
*G*<sub>1</sub> is the max common subgraph of *G*.  
⇐ By definition, *G*<sub>1</sub> is the subgraph of *G* formed by taking
set of *k* independent vertices in the complement of *G* therefore such
an instance exists if there is an independent set of size *k* in the
complement of *G*.  
∴ MCG is NP-complete.