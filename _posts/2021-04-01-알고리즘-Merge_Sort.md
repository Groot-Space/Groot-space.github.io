---
title: "Merge Sort"
excerpt: "재귀를 이용한 Merge Sort와 시간복잡도에 대한 설명입니다."
categories:
    - 알고리즘
    - 파이썬
tags:
    - 정렬
    - BOJ
    - 느낀점
toc: true
toc_sticky: true
use_math: true
---

## 1. 참고한 자료 및 출처
백트래킹에 관련된 글은 [바킹독님 블로그](https://blog.encrypted.gg/955?category=773649)를 참고하였음을 밝힙니다.

## 2. Merge Sort란 ?
1. 재귀적으로 수열을 나눠 정렬한 후 합치는 정렬방법입니다.
2. 기존 삽입, 선택, 버블 정렬들과 비교해 시간복잡도가 O(NlogN)에 수행되는 알고리즘인 만큼 빠르게 정렬이 가능합니다.
3. 코딩테스트에서는 보통 sort()함수를 사용하지만, 면접에서 자주 등장하는 알고리즘인 만큼, 학습해 둘 필요가 있습니다.

## 3. 프로세스 설명.
1. Merge Sort 알고리즘은 1.분해, 2.정렬, 3.합치기의 3가지 프로세스가 재귀적으로 진행이 됩니다. 
2. 알고리즘 구현을 위해서는 O(1)에 정렬된 2개의 배열을 정렬하면서 합치는 방법과 재귀를 사용할 줄 알아야 합니다.

### 1. 정렬된 2개의 배열을 O(1)시간에 정렬하면서 합치는 방법.
![image1](/assets/images/merge_0.jpg)
* 비교하는 횟수를 보시면, 두개의 배열의 크기와 비슷하게 흘러가는 것을 알 수 있습니다.
![image2](/assets/images/merge_1.jpg)
![image3](/assets/images/merge_2.jpg)
![image4](/assets/images/merge_3.jpg)
* 파란 색 배열의 6과 중황 색 배열의 6이 같은 수 입니다. 그림 상에선 귀찮아서 그냥 초록색 배열에 같으면 6, 6연속되게 넣었지만, 실제 코딩에서는 $>=$로 처리하기 때문에 두 개가 동시에 들어가진 않습니다. 
![image5](/assets/images/merge_4.jpg)
![image6](/assets/images/merge_5.jpg)
![image7](/assets/images/merge_6.jpg)
![image8](/assets/images/merge_7.jpg)
![image9](/assets/images/merge_8.jpg)

* 정렬된 2개의 배열을 합치는 이 방법은 Merge Sort의 3가지 프로세스 중 2. 정렬과 3. 합치기에 사용이 됩니다.

### 2. Merge Sort에서 재귀 사용하기.
1. Merge Sort는 위에 설명과 밑에 그림과 같이 1. 분해, 2. 정렬, 3.합치기의 3가지 프로세스로 이뤄집니다.

![image10](/assets/images/Merge_9.jpg)

2. 앞서 설명한 **"정렬된 2개의 배열을 O(1)시간에 정렬하면서 합치는 방법"**을 이용하면 2. 정렬과 3. 합치기 과정에서 자연스럽게 정렬이 되는 것을 알 수 있습니다. 단, **정렬된 2개의 배열**이 존재할 경우를 전제로 하기 때문에, 1. 분해 단계에서 배열의 크기가 1이 될 때까지 분해를 해 줄 필요가 생기게 됩니다. 또, 배열이 1이 되는 조건이 재귀의 Base Condition이 됩니다.

3. 바로 코드 설명으로 넘어가겠습니다.

```python
def merge_sort(arr,st,ed,ret): #인자 값 : 정렬해야 하는 배열, 배열의 시작, 배열의 끝, 정렬 결과를 담을 배열.
    if st+1 == ed: # 배열 길이가 1이면 재귀 종료
        return arr
    m = (ed + st) // 2 # 배열의 중앙 값
    # 배열의 좌측 분리가 끝나면, 우측 분리를 시작함.
    arr = merge_sort(arr, st, m, ret) #배열의 좌측 분리
    arr = merge_sort(arr, m, ed, ret) #배열의 우측 분리
    
    # 배열이 전부 1로 분리가 끝난 상황.
    _idx1 = st #분리된 2개의 배열 중 첫 번째 배열의 시작점 
    _idx2 = m #분리된 2개의 배열 중 두 번째 배열의 시작점
    for i in range(st,ed):
        if _idx1 == m: # for문을 순회하면서, 첫 번째 배열의 idx가 끝까지 오면, 두 번째 배열을 비교 없이 다 집어 넣으면 됨.
            ret[i] = arr[_idx2]
            _idx2 += 1

        elif _idx2 == ed: # 위에 if문과 반대로 두 번째 배열이 끝났으면 첫 번째 배열을 ret에 다 집어넣으면 됨.
            ret[i] = arr[_idx1]
            _idx1 += 1

        elif arr[_idx1] <= arr[_idx2]: # 첫 번째 배열과 두 번째 배열을 비교하면서, 첫 번째 배열의 요소가 두 번째 배열의 요소보다 작거나 같으면 첫 번째 배열을 ret에 집어 넣음.
            ret[i] = arr[_idx1]
            _idx1 += 1

        elif arr[_idx1] > arr[_idx2]: # 위에 elif문과 반대.
            ret[i] = arr[_idx2]
            _idx2 += 1

    for i in range(st,ed): #ret에 있는 정렬된 요소를 arr에 갱신.
        arr[i] = ret[i]

    return arr
```
## 4. 시간복잡도
해당 알고리즘의 시간복잡도는 [소소한 개발공간 임경원의 보조기억장치](https://devlimk1.tistory.com/138)를 참고하시면 되겠습니다.

## 5. 느낀 점
* 재귀 알고리즘을 사용해 Merge Sort를 구현해 봤습니다. 이 알고리즘은 벌써 3~4번 째 구현을 해봤지만, 매번 볼 때마다 새로운 것 같습니다.

* 시간복잡도 부분이 바킹독님 설명과 타 블로그 설명이 조금씩 달라서, 알아 본 후 수정 및 업로드 예정입니다.