---
title: "그래프"
excerpt: "코드 상에서 그래프를 어떻게 다뤄야 할지를 다룹니다."
categories:
    - 알고리즘
    - 파이썬
    - cpp
    - 코딩테스트
tags:
    - 그래프
    - BOJ
    - 느낀점
toc: true
toc_sticky: true
use_math: true
---
## 1. 그래프란?
* 컴퓨터 공학에서 다루는 그래프는 아래 그림과 같은 막대 차트 등의 시각적 자료와 전혀 상관이 없습니다.

![image1](/assets/images/그래프/슬라이드1.jpg)

* 컴퓨터 공학에서 다루는 그래프는 이산수학 / 수리논리학에서 다루는 자료구조 그래프이며, 아래 그림과 같은 모습을 띄고 있습니다.

![image2](/assets/images/그래프/슬라이드2.jpg)

* 그래프는 당장 그래프만으로 코딩테스트에 출제되지는 않으나, 네비게이션에서 최단경로 찾기, 검색엔진에서 랭킹 산정하기 등과 같이 객체 사이의 연결 관계를 설정해야 하는 상황에서 유용하게 활용할 수 있는 자료구조입니다. 또한, 앞으로 배울 플로이드, 다익스트라 알고리즘 혹은 MST(최소신장트리) 등의 내용에서 기초가 되므로 정확하게 익혀두실 필요가 있습니다.

### 1. 그래프 용어 설명.
* **정점(Node or Vertex)**
![image3](/assets/images/그래프/슬라이드3.jpg)

* **간선(Edge)**
![image4](/assets/images/그래프/슬라이드4.jpg)

* **간선의 수(Degree)**
![image5](/assets/images/그래프/슬라이드5.jpg)

* **무방향 그래프(Undirected Graph)**
![image6](/assets/images/그래프/슬라이드6.jpg)

* **방향 그래프(Directed Graph)**
    * **Indegree** : 해당 노드에 들어오는 간선(Edge) 수를 나타냅니다.
    * **Outdegree** : 해당 노드에서 나가는 간선(Edge) 수를 나타냅니다.

![image7](/assets/images/그래프/슬라이드7.jpg)

* **사이클(Cycle)**
    * **Cyclic Graph** : 그래프 안에 탈출할 수 없는 순환이 존재하는 것.
    * **Acyclic Graph** : 사이클이 존재하지 않는 그래프

![image8](/assets/images/그래프/슬라이드8.jpg)
![image9](/assets/images/그래프/슬라이드9.jpg)

* **완전 그래프(Complete Graph)**
![image10](/assets/images/그래프/슬라이드10.jpg)

* **연결 그래프(Connected Graph)**
![image11](/assets/images/그래프/슬라이드11.jpg)

* **단순 그래프(Simple Graph)**
    * 두 정점 사이의 간선이 1개 이하이고 루프가 존재하지 않는 그래프.
    * 루프 : 한 정점에서 시작하여 같은 정점으로 돌아오는 간선.

![image12](/assets/images/그래프/슬라이드12.jpg)

* 간과하기 쉬운 점.
    1. 그래프는 꼭 연결되어 있을 필요가 없습니다.
    2. 두 정점 사이의 간선이 반드시 1개 이하일 필요가 없습니다.
    2. 간선이 반드시 서로 다른 두 정점을 연결해야 할 필요도 없습니다.

## 2.그래프의 표현 방법.
### 1. 인접 행렬
* 각 정점에 번호가 붙어있다고 할 때, 연결된 두 정점에는 **1**을, 연결되지 않은 두 정점에는 **0**을 표시하면 됩니다.

* Undirected graph로 예시를 들겠습니다.
![image13](/assets/images/그래프/슬라이드13.jpg)
![image14](/assets/images/그래프/슬라이드14.jpg)

* table[2][3]이 1이라는 뜻은 2에서 3으로 가는 간선이 있다는 뜻입니다.

* 엄밀하게 1 혹은 0으로만 나타내는 경우, 두 점을 잇는 간선이 여러 개일 경우에 문제가 생길 수 있지만, 대부분의 문제에서 주어지는 그래프는 단순 그래프이므로 고려하지 않도록 하겠습니다.


* 인접 행렬로 그래프를 나타내면 정점이 V개이고 간선이 E개일 때 어떤 두점이 연결되어 있는지를 시간복잡도 $O(1)$에 알 수 있습니다.

* 공간복잡도는 가로 세로의 각각 V(정점의 갯수)인 2차원 배열이 필요하니 $O(V^2)$의 공간이 필요합니다.

* 어떤 정점이 연결되어 있는 모든 목록을 알아내고 싶을 때, 갯수와 무관하게 시간복잡도가 O(V)가 됩니다.

#### 1. 코드

* 지금까지 알고리즘 포스팅에서 다뤘던 코드들은 대부분 python기반으로 다뤘었습니다. python기반으로 다룬데에는 크게 두가지 이유가 있습니다. 1. 가시성, 2. C언어 혹은 cpp와 크게 차이가 없을 것 같기 때문. 하지만, 그래프의 표현법에서는 기본 자료형으로 list를 제공하는 python과 cpp의 차이가 크기 때문에 원초적인 지식함향을 위해 cpp코드도 함께 다루도록 하겠습니다.

* 정점의 갯수 V와 간선의 갯수 E가 주어진 후, E줄에 걸쳐 간선이 주어진다고 가정합니다. 이러한 입력 방식은 코딩 문제의 대부분의 문제에서 사용하고 있는 입력 형식입니다. 이 때 간선을 입력 받으면서 adj_matrix 변수에 1을 적절하게 갱신해주기만 하면 됩니다. 간선이 단방향일 경우 adj_matrix[u][v]만 1로 만들고, 양방향일 경우에는 adj_matrix[u][v], adj_matrix[v][u]를 모두 1로 만들면 됩니다.

* **Directed Graph**일 경우.

```cpp
int adj_matrix[10][10] = {};
int v, e; //정점과 간선의 갯수.
cin >> v >> e;
for(int i = 0; i < e; i++){
    int u, v;
    cin >> u >> v;
    adj_matrix[u][v] = 1;
}
```

```python
from sys import stdin
v, e = list(map(int,stdin.readline().split()))
adj_matrix = [[0 for i in range(v+1)] for j in range(v+1)]
for i in range(e):
    u, v = list(map(int, stdin.readline().split()))
    adj_matrix[u][v] = 1
```

* **Undirected Graph**일 경우

```cpp
int adj_matrix[10][10] = {};
int v, e;
cin >> v >> e;
for(int i = 0; i < e; i++){
    int u, v;
    cin >> u >> v;
    adj_matrix[u][v] = 1;
    adj_matrix[v][u] = 1;
}
```

```python
from sys import stdin
v, e = list(map(int,stdin.readline().split()))
adj_matrix = [[0 for i in range(v+1)] for j in range(v+1)]
for i in range(e):
    u, v = list(map(int, stdin.readline().split()))
    adj_matrix[u][v] = 1
    adj_matrix[v][u] = 1
```

### 2.인접 리스트(Adjacency List)
* 인접 리스트 방식은 인접 행렬과 비교했을 때, V(정점)이 크고 E(간선)이 상대적으로 작은 상황에서 공간을 절약할 수 있는 방식입니다.

* 코딩테스트에서는 인접 행렬보다 훨씬 많이 사용해야 하는 방식입니다.

![image15](/assets/images/그래프/슬라이드15.jpg)
![image16](/assets/images/그래프/슬라이드16.jpg)

* Directed Graph일 경우에는 한 쪽만 넣어주면 됩니다.

* 인접 리스트에서는 O(V + E)의 공간이 필요합니다.

#### 1.코드
* STL을 사용할 수 있는 경우.(방향 그래프)

```cpp
vector<int> adj[10];
int v, e;
cin >> v >> e;
for(int i = 0; i < e; i++){
    int u, v;
    cin >> u >> v;
    adj[u].push_back(v);
}
```

```python
from sys import stdin
v, e = list(map(int,stdin.readline().split()))
adj_matrix = [[] for i in range(v+1)]
for i in range(e):
    u, v = list(map(int, stdin.readline().split()))
    adj_matrix[u].append(v)

```

* STL을 사용할 수 있는 경우.(무방향 그래프)

```cpp
vector<int> adj[10];
int v,e;
cin >> v >> e;
for(int i = 0; i < e; i++){
    int u, v;
    cin >> u >> v;
    adj[u].push_back(v);
    adj[v].push_back(u);
}
```

* STL을 사용할 수 없는 경우(방향 그래프)

```cpp
int edge[10][10];
int deg[10]; // 각 정점의 outdegree
int* adj[10];
int idx[10]; // adj[i]에서 새로운 정점을 추가할 때의 위치
int main(){
    int v, e;
    cin >> v >> e;
    for(int i = 0; i < e; i++){
        cin >> edge[i][0] >> edge[i][1];
        deg[edge[i][0]]++;
    }
    for(int i = 1; i <= v; i++){
        adj[i] = new int[deg[i]];
    }
    for(int i = 0; i < e; i++){
        int u = edge[i][0], v = edge[i][1];
        adj[u][idx[u]] = v;
        idx[u]++;
    }
}
```

* STL을 사용할 수 없는 경우(무방향 그래프)

```cpp
int edge[10][10];
int deg[10]; // 각 정점의 outdegree
int* adj[10];
int idx[10]; // adj[i]에서 새로운 정점을 추가할 때의 위치
int main(){
    int v, e;
    cin >> v >> e;
    for(int i = 0; i < e; i++){
        cin >> edge[i][0] >> edge[i][1];
        deg[edge[i][0]]++;
        deg[edge[i][1]]++;
    }
    for(int i = 1; i <= v; i++){
        adj[i] = new int[deg[i]];
    }
    for(int i = 0; i < e; i++){
        int u = edge[i][0], v = edge[i][1];
        adj[u][idx[u]] = v;
        idx[u]++;
        adj[v][idx[v]] = u;
        idx[v]++;
    }
}
```
### 3.인접 행렬과 인접 리스트의 비교

![image17](/assets/images/그래프/슬라이드17.jpg)
