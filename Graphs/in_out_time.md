## In Out Times of Nodes

The concept of `in` time and and `out` time of a node is pretty simple. It is also referred to as `entry` and `exit` times of a node. 

These times are generally used in several different algorithms to basically determine the ancestor of a given node by comparing the `in` and `out` times of the nodes in question.

This time will be helpful in question designed with `in` and `out` times in mind such as determining whether a specific node is in the subtree of another node or not, as well as when we implement the algorithms for `finding bridges and articulation points`.

## Video Resource for a Quick Primer


 
{% include youtubePlayer.html id="G0N7j-x3YT4" %}


<br><br>

## Few Additional Tips:

* Works for both directed and undirected graphs.

* The In Time refers to the time when a node is first visited and the out time refers to the time when we finally leave that node, when all the explorations from that node has been done.

* Useful for question where it is asked, given two nodes, determine whether they are within each other's subtree or not.

* A node which is in the subtree of other would have in_time greater and out_times lesser than the node of which it is under. 


## Implementation:

```cpp
#include <bits/stdc++.h>
#define lli long long int
#define pii pair<int, int>
#define pb push_back
#define mp make_pair
#define eb emplace_back
#define pf push_front
#define MOD 1000000007
#define F first
#define S second
#define inf INT_MAX
#define gcd(x,y) __gcd(x,y)
#define lcm(a,b) (a*(b/gcd(a,b)))
#define i_am_iron_man ios_base::sync_with_stdio(false);cin.tie(NULL);cout.tie(NULL);

using namespace std;

vector<vector<lli>> graph;
vector<bool> visited;
vector<lli> vec_in;
vector<lli> vec_out;

lli timer = 1;

void addEdge(lli u, lli v)
{
	graph[u].eb(v);
	graph[v].eb(u);
}

void in_out_dfs(lli node)
{
	visited[node] = true;
	vec_in[node] = timer++;
	for(lli i: graph[node])
		if(!visited[i])
			in_out_dfs(i);
	vec_out[node] = timer++;
}

int main()
{
	i_am_iron_man
	lli test;
	cin >> test;
	while(test--)
	{
		lli timer = 1;
		lli n, e;
		cin >> n >> e;
		graph.assign(n, vector<lli>());
		visited.assign(n, false);
		vec_in.assign(n, 0);
		vec_out.assign(n, 0);
		while(e--)
		{
			lli u, v;
			cin >> u >> v;
			addEdge(--u, --v);
		}
		lli source = 1;
		--source;
		in_out_dfs(source);
		for(lli i: vec_in)
			cout << i << " ";
		cout << endl;
		for(lli i: vec_out)
			cout << i << " ";
		cout << endl;
	}
	return 0;
}
``` 
## Sample Input:

```
1
5 4
1 2
2 3
2 4
4 5
```
## Expected Output:

```
1 2 3 5 6 
10 9 4 8 7 
```