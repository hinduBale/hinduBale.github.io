# Depth First Search

Depth First Search is one of the main graph algorithms.

Depth First Search finds the lexicographical first path in the graph from a source vertex $u$ to each vertex.
Depth First Search will also find the shortest paths in a tree (because there only exists one simple path), but on general graphs this is not the case.

The algorithm works in `O(m + n)` time where `n` is the number of vertices and $m$ is the number of edges.

## Video Resources for a Quick Primer

 
{% include youtubePlayer.html id="pcKY4hjDrxk" %}


</br></br>
## Official Description of the algorithm

The idea behind DFS is to go as deep into the graph as possible, and backtrack once you are at a vertex without any unvisited adjacent vertices.

It is very easy to describe / implement the algorithm recursively:
We start the search at one vertex.
After visiting a vertex, we further perform a DFS for each adjacent vertex that we haven't visited before.
This way we visit all vertices that are reachable from the starting vertex.

For more details check out the implementation.

## My Understanding { Don't judge me on this :sob: }

#### Data Structure Used: 
* Breadth means long, and long means queue
* Deapth means deep, and deap means stack.

#### Intuition:
* Depth first means, wherever you start from, keep on going deeper and deeper till you reach the end (leaf nodes).
* Now, how do you go deeper? By calling the `dfs(int node)` function.
* So, from whichever node you call the `dfs(int node)` function set that node as visited and now check for unvisited connections of that particular node which has just been set as visited.
* If you find a connection of that node which is unvisited, you know that you can go deeper by calling `dfs(int node)` on that connection.
* Once you are in such a situation that all connections of a particular node are visited, you can start back-tracking to calculate whatever was being asked in the question.

## Implementation

```cpp
#include <bits/stdc++.h>

#define pb push_back

using namespace std;

vector<vector<int>> graph;
vector<bool> visited;

void addEdge(int u, int v)
{
	graph[u].pb(v);
	graph[v].pb(u);
}

void dfs(int node)
{
	visited[node] = true;
	cout << node << " ";
	for(int i: graph[node])
		if(!visited[i])
			dfs(i);
}

int main()
{
	int test;
	cin >> test;
	while(test--)
	{
		int node, edge;
		cin >> node >> edge;
		graph.assign(node, vector<int>());
		visited.assign(node, false);
		for(int i = 0; i < edge; i++)
		{
			int u, v;
			cin >> u >> v;
			addEdge(u, v);
		}
		dfs(2); //The example I was verifying my code against, required me to set the source as node number 2.
	}
	return 0;
}
```

## Practice Problems (Taken from cp-algorithms)

* [SPOJ: ABCPATH](http://www.spoj.com/problems/ABCPATH/)
* [SPOJ: EAGLE1](http://www.spoj.com/problems/EAGLE1/)
* [Codeforces: Kefa and Park](http://codeforces.com/problemset/problem/580/C)
* [Timus:Werewolf](http://acm.timus.ru/problem.aspx?space=1&num=1242)
* [Timus:Penguin Avia](http://acm.timus.ru/problem.aspx?space=1&num=1709)
* [Timus:Two Teams](http://acm.timus.ru/problem.aspx?space=1&num=1106)
* [SPOJ - Ada and Island](http://www.spoj.com/problems/ADASEA/)
* [UVA 657 - The die is cast](https://uva.onlinejudge.org/index.php?option=com_onlinejudge&Itemid=8&page=show_problem&problem=598)
* [SPOJ - Sheep](http://www.spoj.com/problems/KOZE/)
* [SPOJ - Path of the Rightenous Man](http://www.spoj.com/problems/RIOI_2_3/)
* [SPOJ - Validate the Maze](http://www.spoj.com/problems/MAKEMAZE/)
* [SPOJ - Ghosts having Fun](http://www.spoj.com/problems/GHOSTS/)
* [Codeforces - Underground Lab](http://codeforces.com/contest/781/problem/C)
* [DevSkills - Maze Tester](https://devskill.com/CodingProblems/ViewProblem/3)
* [DevSkills - Tourist](https://devskill.com/CodingProblems/ViewProblem/17)
* [Codeforces - Anton and Tree](http://codeforces.com/contest/734/problem/E)
* [Codeforces - Transformation: From A to B](http://codeforces.com/contest/727/problem/A)
* [Codeforces - One Way Reform](http://codeforces.com/contest/723/problem/E)
* [Codeforces - Centroids](http://codeforces.com/contest/709/problem/E)
* [Codeforces - Generate a String](http://codeforces.com/contest/710/problem/E)
* [Codeforces - Broken Tree](http://codeforces.com/contest/758/problem/E)
* [Codeforces - Dasha and Puzzle](http://codeforces.com/contest/761/problem/E)
* [Codeforces - Making genome In Berland](http://codeforces.com/contest/638/problem/B)
* [Codeforces - Road Improvement](http://codeforces.com/contest/638/problem/C)
* [Codeforces - Garland](http://codeforces.com/contest/767/problem/C)
* [Codeforces - Labeling Cities](http://codeforces.com/contest/794/problem/D)
* [Codeforces - Send the Fool Futher!](http://codeforces.com/contest/802/problem/K)
* [Codeforces - The tag Game](http://codeforces.com/contest/813/problem/C)
* [Codeforces - Leha and Another game about graphs](http://codeforces.com/contest/841/problem/D)
* [Codeforces - Shortest path problem](http://codeforces.com/contest/845/problem/G)
* [Codeforces - Upgrading Tree](http://codeforces.com/contest/844/problem/E)
* [Codeforces - From Y to Y](http://codeforces.com/contest/849/problem/C)
* [Codeforces - Chemistry in Berland](http://codeforces.com/contest/846/problem/E)
* [Codeforces - Wizards Tour](http://codeforces.com/contest/861/problem/F)
* [Codeforces - Ring Road](http://codeforces.com/contest/24/problem/A)
* [Codeforces - Mail Stamps](http://codeforces.com/contest/29/problem/C)
* [Codeforces - Ant on the Tree](http://codeforces.com/contest/29/problem/D)
* [SPOJ - Cactus](http://www.spoj.com/problems/CAC/)
* [SPOJ - Mixing Chemicals](http://www.spoj.com/problems/AMR10J/)
