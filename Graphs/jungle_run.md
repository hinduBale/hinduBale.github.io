## [Jungle Run: ](https://www.hackerearth.com/practice/algorithms/graphs/depth-first-search/practice-problems/algorithm/jungle-run/)
You are lost in a dense jungle and it is getting dark. There is at least one path that leads you to the city on the other side but you cannot see anything until you are right in front of it as the trees and bushes obscure the path.

Devise an algorithm that is guaranteed to find the way out. Your goal is to go out of the jungle as fast as you can before it gets dark.

## Input:
Input start with a number N and then the matrix of size N x N filled with S, E, T, and P which is our map. Map contains a single S representing the start point, and single E representing the end point and P representing the path and T representing the Tree.

## Output:
output single integer i.e. minimum number of moves from S to E.

## Assumptions:
You can assume that the maps would be in square form and can be up to a maximum size of 30X30. You can move in four directions North East West South.
You can move in any direction when you find P but cannot move to a point where a T is present.

## Video Resource for a quick primer:

{% include youtubePlayer.html id="cLE4CQDb10U" %}


<br><br>

## Accepted Solution:

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
#define endl "\n"
#define inf INT_MAX
#define gcd(x,y) __gcd(x,y)
#define lcm(a,b) (a*(b/gcd(a,b)))
#define i_am_iron_man ios_base::sync_with_stdio(false);cin.tie(NULL);cout.tie(NULL);

using namespace std;

char grid[100][100];
int dist[100][100];
int N;
bool visited[100][100];

bool isValid(int x, int y)
{
    if(x < 1 or x > N or y < 1 or y > N)
        return false;
    if(visited[x][y] or grid[x][y] == 'T')
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
}

int main()
{
    i_am_iron_man
    int a, b, c, d;
    cin >> N;
    for(int i = 1; i <= N; i++)
    {
        for(int j = 1; j <= N; j++)
        {
            cin >> grid[i][j];
            if(grid[i][j] == 'S')
            {
                a = i;
                b = j;
            }
            if(grid[i][j] == 'E')
            {
                c = i;
                d = j;
            }
        }
    }
   // cout << N << " " << a << " " << b << " " << c << " " << d << endl;
     bfs(a, b);
     cout << dist[c][d] << endl;
    //cout << a << " " << b;
    return 0;
}
```