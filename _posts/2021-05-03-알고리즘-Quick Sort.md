---
title: "Quick Sort"
excerpt: "Quick Sort에 대한 설명을 다룹니다."
categories:
    - 알고리즘
    - 파이썬
tags:
    - 정렬
toc: true
toc_sticky: true
use_math: true
---

## 1. 참고한 자료 및 출처
Quick Sort에 관련된 글은 [바킹독님 블로그](https://blog.encrypted.gg/955?category=773649)를 참고하였음을 밝힙니다.

## 2. Quick Sort란 ?
1. 재귀 코드로 정렬을 수행하는 알고리즘입니다.
2. 매 단계마다 Pivot이라고 이름을 붙인 원소 하나를 제자리로 보내는 반복 재귀 코드로 구현됩니다. *Pivot : 기준이ㅣ 되는 index*, *제자리에 보낸다 : Pivot기준 오른 쪽에는 Pivot보다 큰 원소가, 왼쪽에는 작은 원소가 오게끔 하는 것*

## 3. 프로세스 & 아이디어 설명.

* 아래의 그림처럼 임시배열 temp를 만들고 Pivot을 제외한 나머지 원소들을 순회하면서 Pivot 이하 값들을 다 temp에 담은 후, Pivot을 담고 다시 한 번 순회하면서 Pivot보다 큰 값들을 temp에 넣어주는 것을 반복하면 된다. 

![image1](/assets/images/quick_sort_0.jpg)
![image2](/assets/images/quick_sort_1.jpg)
![image3](/assets/images/quick_sort_2.jpg)
<br/>

* 그러나, 이렇게 구현하면 Quick Sort의 장점인 "추가적인 공간이 필요하지 않다."가 없어지고, 배열 안에서의 자리바꿈으로 처리되는 장점인, "**Cache hit rate**가 높아서 속도가 빠르다."도 잃게 된다.

* 이러한 장점을 유지하기 위해, 추가적인 공간을 사용하지 않고 정렬하는 **In-Place Sort기법**을 Quick Sort에서는 사용한다.

### 1. 개선한 Quick Sort.
* 변수 설명
    * Left : Pivot보다 큰 값이 나올 때까지 오른 쪽으로 이동, Right을 만나면 멈춰야 합니다.
    * Right : Pivot보다 작은 값이 나올 때까지 왼 쪽으로 이동, Left를 만나도 지나칠 수 있으며, Pivot을 만나면 멈춰야 합니다.
* 알고리즘
    1. Left와 Right이 이동하다가 멈추면, Left와 Right을 서로 교환합니다.
    2. Left와 Right이 교차하게 되면 *(Right이 Pivot을 만나기 전에 작은 값을 만나면)* Pivot과 Right을 교환합니다.
    3. Right이 Pivot과 만나게 되면, 그 상태로 종료하고 새로운 재귀로 들어갑니다.
    4. 배열의 크기가 1이 되면 재귀를 종료합니다.

![image4](/assets/images/quick_sort_3.jpg)
![image5](/assets/images/quick_sort_4.jpg)
![image6](/assets/images/quick_sort_5.jpg)



### 2. Quick Sort 시간복잡도.
* Pivot을 각 단계마다 적절한 위치에 찾아줘야 하므로 **O(N)**
* Pivot 기준으로 배열이 반으로 나뉘어 재귀를 취하므로 반복되는 횟수는 평균 **logN**에 수렴합니다.
* 이미 정렬되어 있는 배열의 경우, 모든 index가 Pivot이 되게 되며 이로 인해 최악의 경우 **$N^2$**의 시간복잡도를 가지게 됩니다.
* STL에서는 최악의 경우에도 **O(NlogN)**을 보장하기 위해 Pivot을 랜덤하게 선택하거나, Pivot후보를 3개 정해서 그 3개 중 중앙 값을 Pivot으로 선택하거나, 일정 깊이 이상 들어가면 Quick Sort 대신 힙소트로 **정렬(Introspective Srot)**을 합니다.
