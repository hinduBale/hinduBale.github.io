# Breadth first search on a Grid

Breadth first search is one of the basic and essential searching algorithms on graphs.

As a result of how the algorithm works, the path found by breadth first search to any node is the shortest path to that node, i.e the path that contains the smallest number of edges in unweighted graphs.

The algorithm works in `O(n + m)` time, where `n` is number of vertices and `m` is the number of edges.

## Video Resources for a Quick Primer

 
{% include youtubePlayer.html id="M4xxztqh8rQ" %}


<br><br>

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

For the intuition behind the DFS Algorithm, check out [this post](./bfs.md).

This is simply the implementation of Breadth First Search on a Grid/Matrix instead of a traditional graph. Getting acquainted with this helps solve a whole new slew of questions, which had previously been unapproachable. In a grid, edges are formed between two cells that are adjacent or even diagonally, depending upon the specifics of the question. No major change is introduced apart from the fact that:
* The visited array becomes 2D (Take care, 2D bool vectors can't be very big, so declare their size conservatively)
* Most probably you would be able to solve these type of questions without explicity declaring a 2D matrix for storing the graph/grid.
* In contrast to traditional graphs, with these grids you have the surity as to what the other connections(connected cells) are.
* The queue used in the bfs becomes a `queue<pair<int, int>>` instead of the traditional `queue<int>`.

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
#define pf push_front
#define MOD 1000000007
#define F first
#define S second
#define inf INT_MAX
#define gcd(x,y) __gcd(x,y)
#define lcm(a,b) (a*(b/gcd(a,b)))
#define i_am_iron_man ios_base::sync_with_stdio(false);cin.tie(NULL);cout.tie(NULL);

using namespace std;

int dist[100][100];
int N, M;
bool visited[100][100];

bool isValid(int x, int y)
{
    if(x < 1 or x > N or y < 1 or y > M)
        return false;
    if(visited[x][y])
        return false;
    return true;
}

int dx[4] = {-1, 0, 1, 0};
int dy[4] = {0, 1, 0, -1};

void bfs(int x, int y)
{
    queue<pii> q;
    q.push({x, y});
    visited[x][y] = true;
    dist[x][y] = 0;
    while(!q.empty())
    {
        int X = q.front().F;
        int Y = q.front().S;

        q.pop();

        for(int i = 0; i < 4; i++)
        {
            if(isValid((X + dx[i]), (Y + dy[i])))
            {
                dist[X + dx[i]][Y + dy[i]] = dist[X][Y] + 1;
                visited[X + dx[i]][Y + dy[i]] = true;
                q.push({X + dx[i], Y + dy[i]});
            }
        }
    }
    for(int i = 1; i <= N; i++){
        for(int j = 1; j <= M; j++)
            cout << dist[i][j] << " ";
        cout << endl;
    }
}

int main()
{
    i_am_iron_man
    int x, y;
    cin >> N >> M;
    cin >> x >> y;
    bfs(x, y);
    return 0;
}
```

## Sample Input:
4 4
1 1

## Expected Output:
0 1 2 3 
1 2 3 4 
2 3 4 5 
3 4 5 6 

## Practice Problems (Taken from cp-algorithms)

* [HackerEarth: Jungle Run](https://www.hackerearth.com/practice/algorithms/graphs/depth-first-search/practice-problems/algorithm/jungle-run/)
