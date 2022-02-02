---
title: "Radix Sort"
excerpt: "기수정렬에 대한 설명을 다룹니다."
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
Radix Sort에 관련된 글은 [바킹독님 블로그](https://blog.encrypted.gg/966?category=773649)를 참고하였음을 밝힙니다.

## 2. Radix Sort(기수정렬)란 ?
1. 자릿수를 이용해 정렬을 수행하는 알고리wma입니다.
2. 시간복잡도는 자릿수 = D, 리스트 개수 = K 라고 할 때, O(D(N+K))시간에 정렬이 가능하지만 K는 N에 비해 무시가 가능할 정도로 작기 때문에 O(DN)으로 표기합니다.

## 3. 프로세스 & 아이디어 설명.

![image1](/assets/images/radix sort/radix_0.jpg)
![image2](/assets/images/radix sort/radix_1.jpg)
![image3](/assets/images/radix sort/radix_2.jpg)
![image4](/assets/images/radix sort/radix_3.jpg)
![image5](/assets/images/radix sort/radix_4.jpg)


### 1. 100의 자릿수부터 배열에 넣으면 안되는 이유.
* 100의 자릿수부터 넣으면 안되는 이유는 100의 자릿수 후 10의 자릿수 -> 1의 자릿수 방식으로 정렬을 하게 되면, 직전 자릿수를 통해 정렬했던 의미가 사라지기 때문입니다.

* 시뮬레이션을 통해 확인해보겠습니다.
![image6](/assets/images/radix sort/radix_5.jpg)
![image7](/assets/images/radix sort/radix_6.jpg)
![image8](/assets/images/radix sort/radix_7.jpg)
</br>

* 이처럼 전혀 정렬이 안되는 것을 확인할 수 있습니다.

## 4. 느낀점 & 어떤 정렬이 좋나?.
* 그림을 보시면 알겠지만, Radix Sort에는 링크드리스트 개념이 들어갑니다. C, C++, JAVA로 구현한다고 가정했을 때, STL을 사용해야 구현이 편한데, STL을 사용할 수 있는 환경에선 구태여 Radix Sort를 구현하는 것보다 STL_SORT를 사용하는 것이 편리하며, python의 경우에는 기본적으로 sort함수가 있기 때문에 구현의 필요성이 희석됩니다.

### 1. Comparison Sort vs Non-comparison Sort
* Sort중에서는 이미 다뤘던 Merge Sort부터 버블, 퀵, 카운팅, 라딕스등의 Sort방법들이 있습니다. 이 방법들은 크게 2가지 차이로 인해 나눌 수 있는데 **원소 간의 비교가 이뤄지냐?(comparison)** 아니면 **원소 간의 비교가 없냐(Non-comparison)**으로 나뉩니다.

* Comparison에 포함되는 정렬은 **Merge Sort**, **버블 정렬**, **퀵 정렬**등이 있습니다.

* Non-Comparison에 포함되는 정렬은 **카운팅 소트**, **Radix Sort** 등이 있습니다.

### 2. 어떤 정렬이 좋냐?
* 그렇다면 마지막으로 코딩테스트에서 정렬을 해야 한다면, 위의 정렬 중에 어떤걸 써야 할까요??, 정답은 이미 아실 거라 생각됩니다. 혹시라도 정 모르시겠다면... xogusxogus39@naver.com으로 메일을 남겨주시면 되겠습니다.. 