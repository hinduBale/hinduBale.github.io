# Depth First Search on a Grid

Depth First Search is one of the main graph algorithms.

Depth First Search finds the lexicographical first path in the graph from a source vertex $u$ to each vertex.
Depth First Search will also find the shortest paths in a tree (because there only exists one simple path), but on general graphs this is not the case.

The algorithm works in `O(m + n)` time where `n` is the number of vertices and $m$ is the number of edges.

## Video Resources for a Quick Primer

 
{% include youtubePlayer.html id="r7-T3Xe3UeI" %}


## Official Description of the algorithm

The idea behind DFS is to go as deep into the graph as possible, and backtrack once you are at a vertex without any unvisited adjacent vertices.

It is very easy to describe / implement the algorithm recursively:
We start the search at one vertex.
After visiting a vertex, we further perform a DFS for each adjacent vertex that we haven't visited before.
This way we visit all vertices that are reachable from the starting vertex.

For more details check out the implementation.

## My Understanding { Don't judge me on this :sob: }

For the intuition behind the DFS Algorithm, check out [this post](./dfs.md).

This is simply the implementation of Depth First Search on a Grid/Matrix instead of a traditional graph. Getting acquainted with this helps solve a whole new slew of questions, which had previously been unapproachable. In a grid, edges are formed between two cells that are adjacent or even diagonally, depending upon the specifics of the question. No major change is introduced apart from the fact that:
* The visited array becomes 2D (Take care, 2D bool vectors can't be very big, so declare their size conservatively)
* Most probably you would be able to solve these type of questions without explicity declaring a 2D matrix for storing the graph/grid.
* In contrast to traditional graphs, with these grids you have the surity as to what the other connections(connected cells) are.

## Implementation

```cpp
/*short and int: -32,767 to 32,767
**unsigned short int and unsigned int: 0 to 65,535
**long int: -2,147,483,647 to 2,147,483,647
**unsigned long int: 0 to 4,294,967,295
**long long int: -9,223,372,036,854,775,807 to 9,223,372,036,854,775,807
**unsigned long long int: 0 to 18,446,744,073,709,551,615.*/

#pragma optimize('O3')
#include <bits/stdc++.h>
#define lli long long int
#define pii pair<int, int>
#define pb push_back
#define mp make_pair
#define eb emplace_back
#define endl "\n"
#define pf push_front
#define MOD 1000000007
#define F first
#define S second
#define inf INT_MAX
#define gcd(x,y) __gcd(x,y)
#define lcm(a,b) (a*(b/gcd(a,b)))
#define i_am_iron_man ios_base::sync_with_stdio(false);cin.tie(NULL);cout.tie(NULL);

using namespace std;

int n, m;
bool visited [1005][1005];

bool isValid(int x, int y)
{
	if(x > n or x < 1 or y > m or y < 1)
		return false;

	if(visited[x][y])
		return false;

	return true;
}

void dfs(int x, int y)
{
	visited[x][y] = true;
	cout << x << " " << y << endl;

	if(isValid(x-1, y))
		dfs(x-1, y); //Move Up

	if(isValid(x, y+1))
		dfs(x, y+1); //Move Right

	if(isValid(x+1, y))
		dfs(x+1, y); //Move down

	if(isValid(x, y-1))
		dfs(x, y-1); //Move Left
}

int main()
{
	i_am_iron_man
	cin >> n >> m;
	dfs(1, 1);
	return 0;
}
```

A simpler approach, so that in case diagonal connections are allowed, you don't have to write up eight possible conditions for dfs ;)

```cpp
int dx[4] = {-1, 0, 1, 0};
int dy[4] = {0, 1, 0, -1};

void dfs(int x, int y)
{
	visited[x][y] = true;
	cout << x << " " << y << endl;

	for(int i = 0; i < 4; i++)
		if(isValid((x + dx[i]), (y + dy[i])))
			dfs((x + dx[i]), (y + dy[i]));
}
```

## Practice Problems

* [HackerEarth: Jungle Run](https://www.hackerearth.com/practice/algorithms/graphs/depth-first-search/practice-problems/algorithm/jungle-run/)
* [CSES: Counting Rooms](https://cses.fi/problemset/task/1192/)
* [CodeChef: Chess Knight Moves](https://www.codechef.com/PROC2017/problems/PRGCUP01)
