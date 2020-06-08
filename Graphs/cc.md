# Search for connected components in a graph

Given an undirected graph $G$ with $n$ nodes and $m$ edges. We are required to find in it all the connected components, i.e, several groups of vertices such that within a group each vertex can be reached from another and no path exists between different groups.

## Video Resources for a Quick Primer

 
{% include youtubePlayer.html id="z49Ohr5Ypnw" %}


<br><br>

## An algorithm for solving the problem

* To solve the problem, we can use Depth First Search or Breadth First Search.

* In fact, we will be doing a series of rounds of DFS: The first round will start from first node and all the nodes in the first connected component will be traversed (found). Then we find the first unvisited node of the remaining nodes, and run Depth First Search on it, thus finding a second connected component. And so on, until all the nodes are visited.

* The total asymptotic running time of this algorithm is $O(n + m)$ : In fact, this algorithm will not run on the same vertex twice, which means that each edge will be seen exactly two times (at one end and at the other end).

## My Understanding(Don't judge me on this _ /\ _ )

A graph does not always need to be one single entity. Think of a graph like an island nation. It could be a one single entity like Japan or it could be a group of different islands under the aegis of a single country like the Maldives. So, you can think of one single island as a connected component. Now, even though there is no way(land based) to reach from one island to another of the same nation(graph), they are disconnected components of the same graph.

Detection of a connected component is very easy.
Run DFS(or even BFS) on any vertex and if it stops before covering all the vertices, increment the count of connected components.
Repeat this, till each and every node has been traversed by our DFS.

## Implementation

``` cpp
#include <bits/stdc++.h>

#define pb push_back
#define endl "\n"
#define lli long long int
#define i_am_iron_man ios_base::sync_with_stdio(false);cin.tie(NULL);cout.tie(NULL);

using namespace std;

vector<vector<lli>> graph;
vector<bool> visited;

void addEdge(lli u, lli v)
{
	graph[u].pb(v);
	graph[v].pb(u);
}

void dfs(lli node)
{
	visited[node] = true;
	for(lli i : graph[node])
		if(!visited[i])
			dfs(i);
}

int main()
{
	i_am_iron_man
	lli n, e, connected_comp = 0;
	cin >> n >> e;
	graph.assign(n, vector<lli>());
	visited.assign(n, false);
	while(e--)
	{
		lli u, v;
		cin >> u >> v;
		addEdge(--u, --v);
	}
	for(lli i = 0; i < n; i++)
	{
		if(!visited[i])
		{
			++connected_comp;
			dfs(i);
		}
	}
	cout << connected_comp << endl;
	return 0;
}

```

## Solved Question (Easy)

```
/*
#Link to Question:
https://www.hackerearth.com/problem/algorithm/connected-components-in-a-graph/description/

#Question:
Given n, i.e. total number of nodes in an undirected graph numbered from 1 to n and an integer e, i.e. total number of edges in the graph. Calculate the total number of connected components in the graph. A connected component is a set of vertices in a graph that are linked to each other by paths.

Input Format:

First line of input line contains two integers n and e. Next e line will contain two integers u and v meaning that node u and node v are connected to each other in undirected fashion. 

Output Format:

For each input graph print an integer x denoting total number of connected components.

Constraints:

All the input values are well with in the integer range.

*/
```

## Practice Problems
 - [SPOJ: CCOMPS](http://www.spoj.com/problems/CCOMPS/)
 - [SPOJ: CT23E](http://www.spoj.com/problems/CT23E/)
 - [CODECHEF: GERALD07](https://www.codechef.com/MARCH14/problems/GERALD07)
