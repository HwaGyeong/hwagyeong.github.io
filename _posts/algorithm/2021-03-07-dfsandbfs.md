---
layout: post
title : "[백준 1260] DFS와 BFS"
subtitle: DFS 재귀 , BFS queue stl 활용
categories:
  - algorithm
tags:
  - [Algorithm ,BOJ,dfs,bfs]
comments: true  
---

### DFS와 BFS

> 문제설명
![image](https://user-images.githubusercontent.com/55472510/110426459-7db9dc80-80e9-11eb-9d19-134fe322c952.png)

기본적인 DFS&BFS를 구현한다. 
이때, 정점의 갯수(N) 간선의 갯수(M), 그리고 시작노드(V)를 입력 받는다. 
dfs와 bfs를 수행하고 난 노드 방문 순서를 출력시킨다.

> 알고리즘 순서
1. DFS의 경우 현재 방문한 노드의 인덱스를 매개변수로 전달 
2. 반복문을 통해서 방문하지 않았고 연결되어 있는 노드를 재귀적으로 방문한다.
3. BFS의 경우도 동일하고 queue에 현재 방문한 노드를 넣는다.
4. 반복문을 통해서 queue가 비어있을 때 까지 맨 앞의 노드를 끄내고, 그 노드와 인접했지만 방문하지 않은 노드를 방문한다.

```cpp
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <iostream>
#include <queue>
using namespace std;
#define MAX 1001

int graph[MAX][MAX];
int N, M, V;
bool visited[MAX];
bool visit[MAX];
void DFS(int index)
{
	cout << index<<" ";//현재 방문한 노드 출력
	visited[index] = 1;

	for (int i = 1; i <= N;i++)//재귀적으로 노드 수만큼 반복 
	{
		if (visited[i] == 0 && graph[i][index]== 1)//방문 안했고, 현재 노드와 연결되어 있는 경우 재귀적으로 방문
			DFS(i);
	}
}

void BFS(int index)
{
	queue <int> q;
	q.push(index);//시작 노드는 방문 처리
	visit[index] = 1;
	while (!q.empty())
	{
		index = q.front();//현재 노드 값 받고 
		cout << q.front() << " ";//방문한 노드 값 출력
		q.pop();//방문 했으니 queue에서 제거 
		for (int i = 1; i <= N; i++)//총 노드 수 만큼 연결관계 조회 
		{
			if (visit[i] == 0 && graph[i][index] == 1)//안갔고 현재노드와 연결되있으면 방문
			{
				q.push(i);//새로 방문한 곳은 queue에 넣기 
				visit[i] = 1;//방문 했다는 표시 남기기
			}
		}
	}
}
int main(void)
{
 	cin >> N >> M >> V;

	int x, y;
	for (int i = 0; i < M; i++)//연결 관계 입력 받기
	{
		cin >> x >> y;
		graph[x][y] = graph[y][x] = 1;
	}

	DFS(V);
	cout << "\n";
	BFS(V);

	return 0;
}

```
이 때 dfs알고리즘의 경우 재귀적인 방법으로 해당노드가 방문되지 않았고 현재노드와 연결관계를 확인하고 방문 하는 방식으로 동작한다.

dfs의 경우 stack으로도 구현이 가능하다.

bfs의 경우 queue stl을 사용하여 (선입선출) 처음 방문하면 queue에 넣고 반복문을 통해서 front값(현재값)을 받고 그 노드와 연결관계와 방문여부를 확인한 뒤 연결되어있으며 방문하지 않은 경우 queue에 넣고 visit여부를 true로 변경한다. 


