---
title: "Union Find"
excerpt: "Union-Find 알고리즘의 이해 및 코딩방법을 설명합니다."
categories:
    - 알고리즘
    - 파이썬
tags:
    - Union Find
    - BOJ
    - 그래프
    - 느낀점
toc: true
toc_sticky: true
use_math: true
---

## 1. Union Find란?
* 그래프 알고리즘의 하나로, 주어진 여러 그래프 중에서 집합을 찾는 알고리즘입니다. 그렇기 때문에 서로소 집합(Disjoint-Set) 알고리즘이라고도 불립니다.

* 예시)

![image1](/assets/images/union_find_0.jpg)

![image2](/assets/images/union_find_1.jpg)

## 2. 알고리즘 프로세스
### 1. 표현 방법 및 Union 과정.
* 그래프를 1차원 배열에 저장하고 사용하게 됩니다. 이 때, 배열의 idx는 노드의 번호가 되며, 배열 안의 값들은 노드가 속해있는 집합의 대표값이 들어가게 됩니다.

* 대표값이란, 노드들의 집합 중 가장 작은 값을 의미합니다.

* 초기값은 각 노드들의 값이 대표값으로 들어가게 됩니다.

* 위 그래프를 예시로 표시하면, 초기화는 다음과 같은 형태가 됩니다.

![image3](/assets/images/Union_find_2.jpg)

* 이후 입력값에 노드 1과 노드 2가 연결되어 있다는 정보가 들어왔다고 예를 들겠습니다. 이 때 노드의 수가 더 큰 쪽의 배열idx에 작은 쪽의 노드 번호의 값을 입력하게 됩니다. **단 배열의 값이 idx의 값과 동일한 경우에 한정됩니다.** 만약, 값이 동일하지 않다면 노드 2는 이미 다른 집합에 소속되어 있다는 뜻이 되므로, 해당 집합의 대표값을 찾아줘야 하는데, 이 과정은 후술하도록 하겠습니다.

* 예제를 가지고 예시를 들면, 노드 1과 노드 2가 연결되어 있다는 정보를 표현할 때 배열[2]의 값이 자기 자신의 idx인 2이며, 노드 2가 노드 1보다 더 크기 때문에, (2 > 1) 배열[2] = 1 이라고 입력을 해줍니다.

![image4](/assets/images/Union_find_3.jpg)

* 다음으로 노드 1과 노드 3이 연결되어 있는 것을 표현하겠습니다. 이 경우에도 위의 경우와 같은 프로세스로 진행해주면 됩니다. 3이 더 큰 번호이며, 배열[3]의 값은 3이기 때문에 아무 문제 없이 배열[3]의 값을 1로 바꿔줍니다.

![image5](/assets/images/Union_find_4.jpg)

* 이제 집합 A의 표현은 끝났습니다. 집합 B를 표현하도록 하겠습니다. 노드 7과 노드 4가 연결되어 있다는 정보가 들어왔을 때, 위와 같은 프로세스로 배열[7]의 값이 7이며, 노드 7이 노드 4보다 크므로 배열[7]의 값을 4로 갱신해줍니다.

![image6](/assets/images/Union_find_5.jpg)

* 노드 6과 노드 5를 연결해 보겠습니다. 위 프로세스와 같은 방식으로 연결해주면 됩니다. 노드 6이 더 크기 때문에 배열[6]에 5를 넣어줍니다.

![image7](/assets/images/Union_find_6.jpg)

* 이제 마지막으로 노드 4와 노드 6을 연결하겠습니다. 노드 6이 더 큰 번호이므로 배열[6]에 4를 추가하고 싶었으나, 배열[6]의 값을 보면 5로 배열 idx와 같지가 않습니다. 즉 노드 6은 이미 다른 집합에 속해있으므로, 노드 6의 집합을 찾아야 합니다.

* 배열[6]의 값을 보면 노드 6이 노드 5의 그룹에 속해있는 것을 알 수 있습니다. 그리고, 배열[5] = 5이므로 5와 6이 한 그룹인 것을 알 수 있습니다. 즉, 노드 5와 노드 4를 연결하게 되면 노드 6과 노드 4도 자연스럽게 연결이 됨을 알 수 있습니다. 그러므로, 노드 5와 노드 4를 연결하도록 하겠습니다. 참고로 이 과정은 재귀적 코드로 구현을 하게 됩니다.

* 노드 5와 노드 4 중 노드 5가 더 크기 때문에, 배열[5]에 4를 넣도록 하겠습니다.

![image8](/assets/images/Union_find_7.jpg)

![image9](/assets/images/Union_find_8.jpg)

* 이로써 예시에 나와있는 집합의 Union과정이 끝났습니다.

### Find 과정

* 이제는 노드 1과 노드 7이 같은 집합에 속해있는지를 확인하는 과정을 예시로, 노드 간의 소속 집합이 같은지를 확인하는 Find 과정을 진행하도록 하겠습니다.

* 노드 1의 집합은 배열[1] = 1이기 때문에 집합 1에 속하는 것을 알 수 있습니다. 노드 7의 경우 배열[7] = 4이기 때문에 노드 4의 집합과 같은 집합에 속해있는 것을 알 수 있습니다. 노드 4가 어떤 집합에 속해 있는지 확인하려면, 배열[4]를 확인하면 되며, 배열[4] = 4이기 때문에 노드 4가 집합의 대표 노드가 되는 것을 알 수 있습니다. 결과적으로는 노드 1의 집합 = 1, 노드 7의 집합 = 4이므로 두 노드는 서로 다른 노드에 소속되어 있습니다.

![image10](/assets/images/Union_find_9.jpg)

## 3. 코드
```python
def get_parent(arr,node): #소속 집합의 대표값을 찾는 과정.
    if arr[node] == node: #노드 번호와 노드가 같을 경우
        return node
    else :
        arr[node] = get_parent(arr, arr[node]) #다를 경우엔, 재귀적으로 소속되어 있는 집합의 대표 노드를 찾아냄.
        return arr[node]

def union(arr, node1, node2): #node1과 node2를 연결시켜주는 과정.
    node1_parent = get_parent(arr, node1)
    node2_parent = get_parent(arr, node2)

    if node1_parent > node2_parent : # 노드 1의 집합 대표와 노드 2의 집합 대표의 대소 비교
        arr[node1_parent] = node2_parent
    else :
        arr[node2_parent] = node1_parent

def find(arr, node1, node2): #node1과 node2의 집합이 같은지 확인.
    node1_parent = get_parent(arr, node1)
    node2_parent = get_parent(arr, node2)
    if node1_parent == node2_parent:
        return True
    else :
        return False
```

## 4.느낀점.
* Union-Find 알고리즘은 이후 포스팅 할 MST(최소신장트리)의 풀이과정에서 크루스칼 알고리즘을 활용할 때, 유용하게 사용이 됩니다. 또한, 코딩테스트에서도 비중이 꽤 있는 문제입니다. 그렇기에 익혀두면 분명 도움이 되는 알고리즘 중에 하나입니다.