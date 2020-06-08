# Breadth-first search
Breadth first search is one of the basic and essential searching algorithms on graphs.

As a result of how the algorithm works, the path found by breadth first search to any node is the shortest path to that node, i.e the path that contains the smallest number of edges in unweighted graphs.

The algorithm works in `O(n + m)` time, where `n` is number of vertices and `m` is the number of edges.

## Video Resources for a Quick Primer

 
{% include youtubePlayer.html id="pcKY4hjDrxk" %}




## Official Description of the algorithm

The algorithm takes as input an unweighted graph and the id of the source vertex `s`. The input graph can be directed or undirected,
it does not matter to the algorithm.

The algorithm can be understood as a fire spreading on the graph: at the zeroth step only the source `s` is on fire. At each step, the fire burning at each vertex spreads to all of its neighbors. In one iteration of the algorithm, the "ring of
fire" is expanded in width by one unit (hence the name of the algorithm).

More precisely, the algorithm can be stated as follows: Create a queue `q` which will contain the vertices to be processed and a
Boolean array `used[]` which indicates for each vertex, if it has been lit (or visited) or not.

Initially, push the source `s` to the queue and set `used[s] = true`, and for all other vertices `v` set `used[v] = false`.
Then, loop until the queue is empty and in each iteration, pop a vertex from the front of the queue. Iterate through all the edges going out
of this vertex and if some of these edges go to vertices that are not already lit, set them on fire and place them in the queue.

As a result, when the queue is empty, the "ring of fire" contains all vertices reachable from the source `s`, with each vertex reached in the shortest possible way.
You can also calculate the lengths of the shortest paths (which just requires maintaining an array of path lengths `d[]`) as well as save information to restore all of these shortest paths (for this, it is necessary to maintain an array of "parents" `p[]`, which stores for each vertex the vertex from which we reached it).

## My Understanding ( Don't judge me on this _ /\ _  )

#### Data Structure Used:
* Breadth means long, and long means queue
* Deapth means deep, and deep means stack.

#### Intuition:

Ok, so breadth first means, be as broad as possible. In stark contrast to the approach taken by DFS we first traverse the breadth of the graph as compared to the depth. So, this method of traversal is also called `level order traversal`. 
Here, we first visit all the nodes in the adjacency list of the source node all the while putting them in a queue. We then move on to the next node from the source node based on the order in the queue. Whichever node is taken as the source node is also popped from the queue.
We keep on iterating as long as the queue is not empty. 

#### Additional Stuff:

In the implementation, I've maintained an array of parents, that is helpful to determine the path from one given node to another. Also, I've maintained a distance array that helps determine the distance between two given nodes.

## Implementation

We write code for the described algorithm in C++.

```cpp
#include <bits/stdc++.h>

#define pb push_back
#define endl "\n"
#define i_am_iron_man ios_base::sync_with_stdio(false);cin.tie(NULL);cout.tie(NULL);

using namespace std;

vector<vector<int>> graph;
vector <bool> visited;
vector <int> dist;
vector <int> parent;

void addEdge(int u, int v)
{
    graph[u].pb(v);
    graph[v].pb(u);
}

void bfs(int source)
{
    queue<int> q;
    q.push(source);
    visited[source] = true;
    dist[source] = 0;
    parent[source] = -1;
    while(!q.empty())
    {
        int f = q.front();
        cout << f << " "; //Or whatever the operation being required here.
        q.pop();
        for(int i: graph[f])
        {
            if(!visited[i])
            {
                visited[i] = true;
                q.push(i);
                dist[i] = dist[f] + 1;
                parent[i] = f;
            }
        }
    }
    cout << endl;
}

void findPath(int node)
{
    if(!visited[node])
        cout << "-1" << endl;
    else
    {
        vector <int> path;
        for(int i = node; i != -1; i = parent[node])
            path.pb(i);
        reverse(path.begin(), path.end());
        cout << "Path: ";
        for(auto i: path)
            cout << i << " ";
        cout << endl;
    }
}

int main()
{
    i_am_iron_man
    int test;
    cin >> test;
    while(test--)
    {
        int node, edge;
        cin >> node >> edge;
        visited.assign(node, false);
        parent.assign(node, -1);
        dist.assign(node, 0);
        graph.assign(node, vector<int>());
        int u, v;
        for(int i = 0; i < edge; i++)
        {
            cin >> u >> v;
            addEdge(u, v);
        }
        for(int i = 0; i < node; i++)
          if(!visited[i])
              bfs(i);
        for(int i = 0; i < node; i++)
            findPath(i);
        //bfs(0);
    }
    return 0;
}
```

## Applications of BFS

* Find the shortest path from a source to other vertices in an unweighted graph.

* Find all connected components in an undirected graph in `O(n + m)` time:
To do this, we just run BFS starting from each vertex, except for vertices which have already been visited from previous runs.
Thus, we perform normal BFS from each of the vertices, but do not reset the array `used[]` each and every time we get a new connected component, and the total running time will still be `O(n + m)` (performing multiple BFS on the graph without zeroing the array `used []` is called a series of breadth first searches).

* Finding a solution to a problem or a game with the least number of moves, if each state of the game can be represented by a vertex of the graph, and the transitions from one state to the other are the edges of the graph.

* Finding the shortest path in a graph with weights 0 or 1:
This requires just a little modification to normal breadth-first search: Instead of maintaining array `used[]`, we will now check if the distance to vertex is shorter than current found distance, then if the current edge is of zero weight, we add it to the front of the queue else we add it to the back of the queue.This modification is explained in more detail in the article [0-1 BFS](graph/01_bfs.html).

* Finding the shortest cycle in a directed unweighted graph:
Start a breadth-first search from each vertex.
As soon as we try to go from the current vertex back to the source vertex, we have found the shortest cycle containing the source vertex.
At this point we can stop the BFS, and start a new BFS from the next vertex.
From all such cycles (at most one from each BFS) choose the shortest.

* Find all the edges that lie on any shortest path between a given pair of vertices `(a, b)`.
To do this, run two breadth first searches:
one from `a` and one from `b`.
Let `d_a []` be the array containing shortest distances obtained from the first BFS (from `a`) and `d_b []` be the array containing shortest distances obtained from the second BFS from `b`.
Now for every edge `(u, v)` it is easy to check whether that edge lies on any shortest path between `a` and `b`:
the criterion is the condition `d_a [u] + 1 + d_b [v] = d_a [b]`.

* Find all the vertices on any shortest path between a given pair of vertices `(a, b)`.
To accomplish that, run two breadth first searches:
one from `a` and one from `b`.
Let `d_a []` be the array containing shortest distances obtained from the first BFS (from `a`) and `d_b []` be the array containing shortest distances obtained from the second BFS (from `b`).
Now for each vertex it is easy to check whether it lies on any shortest path between `a` and `b`:
the criterion is the condition `d_a [v] + d_b [v] = d_a [b]`.

* Find the shortest path of even length from a source vertex `s` to a target vertex `t` in an unweighted graph:
For this, we must construct an auxiliary graph, whose vertices are the state `(v, c)`, where `v` - the current node, `c = 0` or `c = 1` - the current parity.
Any edge `(a, b)` of the original graph in this new column will turn into two edges `((u, 0), (v, 1))` and `((u, 1), (v, 0))`.
After that we run a BFS to find the shortest path from the starting vertex `(s, 0)` to the end vertex `(t, 0)`.

## Practice Problems (Taken from cp-algorithms)

* [SPOJ: AKBAR](http://spoj.com/problems/AKBAR)
* [SPOJ: NAKANJ](http://www.spoj.com/problems/NAKANJ/)
* [SPOJ: WATER](http://www.spoj.com/problems/WATER)
* [SPOJ: MICE AND MAZE](http://www.spoj.com/problems/MICEMAZE/)
* [SPOJ - Spiky Mazes](http://www.spoj.com/problems/SPIKES/)
* [SPOJ - Four Chips (hard)](http://www.spoj.com/problems/ADV04F1/)
* [SPOJ - Inversion Sort](http://www.spoj.com/problems/INVESORT/)
* [Codeforces - Shortest Path](http://codeforces.com/contest/59/problem/E)
* [SPOJ - Yet Another Multiple Problem](http://www.spoj.com/problems/MULTII/)
* [Codeforces - Police Stations](http://codeforces.com/contest/796/problem/D)
* [Codeforces - Okabe and City](http://codeforces.com/contest/821/problem/D)
* [SPOJ - Find the Treasure](http://www.spoj.com/problems/DIGOKEYS/)
* [Codeforces - Bear and Forgotten Tree 2](http://codeforces.com/contest/653/problem/E)
* [Codeforces - Cycle in Maze](http://codeforces.com/contest/769/problem/C)
* [SPOJ - Ada and Cycle](http://www.spoj.com/problems/ADACYCLE/)
