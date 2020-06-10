## Single Source Shortest Path:

So, in this algorithm, we are given a source node and from there we are supposed to find the shortest distance between any and all nodes starting from the source node.

Here, we will be using [DFS](./dfs.md) with a some additional parameters to achieve what we want. So, the time complexity remains as that of DFS: `O(m+n)` where `m` is the number of edges and `n` is the number of vertices.

An important point to note however is that: **This algorithm would only work for trees and not graphs.**

*You can consider a simple graph
```
0 1
0 2
1 2
```
to verify, why this approach won't work on graphs.*

## Video Resource for a Quick Primer


 
{% include youtubePlayer.html id="pcKY4hjDrxk" %}


<br><br>

## Description:

We are basically using the Depth First Search Algorithm here with a little tweaks. So, you could check out the DFS [here](./dfs.md).

We will be maintaining a distance array `dist[]` that will store the distance of all nodes from the source node and hence logically the value of source node in the `dist[] array` would be `0`.
The `dist[] array` is updated whenver the function `dfs(int node`) is called again by adding `1` to the distance of the parent node.

At the end to find the distance of a specific node from the vertex simply *cout* the `dist[index_of_reqd_node]`.

## Implementation:

```cpp
#include <bits/stdc++.h>

#define lli long long int
#define endl "\n"
#define pb push_back

using namespace std;

vector <vector<lli>> graph;
vector <bool> visited;
vector <lli> dist;

void addEdge(lli u, lli v)
{
	graph[u].pb(v);
	graph[v].pb(u);
}

void dfs(lli node)
{
	visited[node] = true;
	for(lli i: graph[node]){
		if(!visited[i]){
			dist[i] = dist[node] + 1;
			dfs(i);
		}
	}
}

int main()
{
	lli n, e;
	cin >> n >> e;
	graph.assign(n, vector<lli>());
	visited.assign(n, false);
	dist.assign(n, 0);
	while(e--)
	{
		lli u, v;
		cin >> u >> v;
		addEdge(--u, --v);
	}
	lli source = 2;
	--source;
	dfs(source);
	for(lli i: dist)
		cout << i << " ";
	cout << endl;
	return 0;
}
```