# Connected Components in a grid

Given a grid(2D Matrix) consisting of 0's and 1's, we have to find the number of connected components, i.e, several groups of vertices such that within a group each vertex can be reached from another and no path exists between different groups. 

Here the connected components are defined such that you could move from one cell to another if they share are adjacent to each other and neither of them is 0. 0 serves as a kind of a roadblock. Now, determine the number of "ghettos" of 1's.

## Video Resources for a Quick Primer

 
{% include youtubePlayer.html id="yu4qdoG3618" %}



## An algorithm for solving the problem

* To solve the problem, we can use Depth First Search or Breadth First Search.

* In fact, we will be doing a series of rounds of DFS: The first round will start from first node and all the nodes in the first connected component will be traversed (found). Then we find the first unvisited node of the remaining nodes, and run Depth First Search on it, thus finding a second connected component. And so on, until all the nodes are visited.

* The total asymptotic running time of this algorithm is `O(n + m)` : In fact, this algorithm will not run on the same vertex twice, which means that each edge will be seen exactly two times (at one end and at the other end).

## My Understanding ( Don't judge me on this _ /\ _  )

For the intuitive sense behind the algorithm to find connected components, please check out [this post](./cc.md).

* The algorithm here remains the same as for traditional graph, it's just that here vertices are replaced by cells of a matrix
* Another thing is that here we have to store the grid in a 2D matrix called `int grid[][]` to deal witht the additional constraint of 0's and 1's.
* Based on the questions slight modifications would have to be made such as maybe replace the 0's and 1's with `#` and `.` .

## Implementation

``` cpp
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
#define endl "\n"
#define gcd(x,y) __gcd(x,y)
#define lcm(a,b) (a*(b/gcd(a,b)))
#define i_am_iron_man ios_base::sync_with_stdio(false);cin.tie(NULL);cout.tie(NULL);

using namespace std;

int n, m;
bool visited[1005][1005];
int grid[1005][1005];

bool isValid(int x, int y)
{
    if(x < 1 or x > n or y < 1 or y > m)
        return false;
    if(visited[x][y] == true or grid[x][y] == 0)
        return false;

    return true;
}

int dx[4] = {-1, 0, 1, 0};
int dy[4] = {0, 1, 0, -1};

void dfs(int x, int y)
{
    visited[x][y] = true;

    for(int i = 0; i < 4; i++)
        if(isValid((x+dx[i]), (y+dy[i])))
            dfs((x+dx[i]), (y+dy[i]));
}

int main()
{
    i_am_iron_man
    cin >> n >> m;

    for(int i = 1; i <= n; i++)
        for(int j = 1; j <= m; j++)
            cin >> grid[i][j];

    int connected_component = 0;

    for(int i = 1; i <= n; i++)
        for(int j = 1; j <= m; j++)
            if(visited[i][j] == false and grid[i][j] == 1)
            {
                ++connected_component;
                dfs(i, j);
            }

    cout << "Number of Connected Components: " <<connected_component << endl;

    return 0;
}
```
## Sample Input:
    
`    6 6
0 0 1 0 1 1
0 1 1 0 0 1
0 1 0 0 0 0
1 0 1 1 0 0
0 0 0 1 0 0
0 1 1 0 1 1`

## Expected Output:
    
    `6`

## Practice Problems (Not necessarily grid cc questions from cp-algorithms)
 - [SPOJ: CCOMPS](http://www.spoj.com/problems/CCOMPS/)
 - [SPOJ: CT23E](http://www.spoj.com/problems/CT23E/)
 - [CODECHEF: GERALD07](https://www.codechef.com/MARCH14/problems/GERALD07)
