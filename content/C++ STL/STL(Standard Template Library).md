# **STL (Standard Template Library)**

STL은 **Generic Programming**을 위한 대표적인 C++ 라이브러리야.

---

## **STL의 4가지 구성 요소**
1. **컨테이너 (Containers)** → 데이터를 저장하는 자료구조
2. **알고리즘 (Algorithms)** → 정렬, 탐색 등의 연산을 수행
3. **함수 객체 (Function Objects)** → 함수처럼 동작하는 객체
4. **반복자 (Iterators)** → 컨테이너의 원소를 순회하는 포인터 역할

---

## **1. 컨테이너 (Containers)**
데이터를 저장하고 관리하는 STL의 기본 요소.

### **컨테이너의 분류**
#### **1) 원소 배치 방식에 따른 분류**
- **시퀀스 컨테이너** → `vector`, `deque`, `list`, `array`, `forward_list`
  - 연속된 메모리 구조를 가짐
- **연관 컨테이너 (정렬됨)** → `set`, `multiset`, `map`, `multimap`
  - 내부적으로 **이진 검색 트리 (RB-Tree)** 사용
- **연관 컨테이너 (비정렬)** → `unordered_set`, `unordered_map`
  - 내부적으로 **해시 테이블** 사용 (빠른 탐색 가능)

#### **2) 메모리 저장 방식에 따른 분류**
- **배열 기반 컨테이너** → `vector`, `deque`
- **노드 기반 컨테이너** → `set`, `map`, `list`

### **컨테이너 어댑터 (Container Adapters)**
기존 컨테이너를 기반으로 **특정 기능만 제공하는 컨테이너**
- `stack` (LIFO)
- `queue` (FIFO)
- `priority_queue` (우선순위 큐)

---

## **2. 알고리즘 (Algorithms)**
- STL에서 제공하는 **정렬, 탐색, 변형 등의 연산 함수 모음**
- `<algorithm>` 헤더를 포함해야 사용 가능
- 컨테이너에 종속되지 않고 범용적으로 활용 가능

**대표적인 알고리즘 예제**
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

int main() {
    std::vector<int> v = {5, 2, 8, 1, 3};
    std::sort(v.begin(), v.end()); // 오름차순 정렬
    for (int num : v) std::cout << num << " ";
    return 0;
}
```

---

## **3. 함수 객체 (Function Object, Functor)**
- 함수처럼 동작하는 객체 (람다식이 등장하면서 사용 빈도 감소)
- 연산자 오버로딩을 활용해 특정 동작 수행 가능

**예제: 사용자 정의 정렬 기준**
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

struct Descending {
    bool operator()(int a, int b) { return a > b; }
};

int main() {
    std::vector<int> v = {5, 2, 8, 1, 3};
    std::sort(v.begin(), v.end(), Descending()); // 내림차순 정렬
    for (int num : v) std::cout << num << " ";
    return 0;
}
```

---

## **4. 반복자 (Iterators)**
- 컨테이너의 요소를 순회하기 위한 객체
- 포인터처럼 동작하지만 포인터가 아님 (`operator*`, `operator->` 오버로딩)

**반복자의 주요 유형**
| 반복자 종류 | 특징 |
|----------------- |----------------------------------|
| 입력 반복자      | 한 방향으로 읽기만 가능 (`cin` 등) |
| 출력 반복자      | 한 방향으로 쓰기만 가능 (`cout` 등) |
| 순방향 반복자 | 한 방향으로 읽고 쓸 수 있음 (`list`, `forward_list`) |
| 양방향 반복자 | 앞뒤로 이동 가능 (`set`, `map`, `list`) |
| 임의 접근 반복자 | 임의의 위치로 이동 가능 (`vector`, `deque`) |

**반복자 예제**
```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> v = {10, 20, 30, 40, 50};
    std::vector<int>::iterator it;
    for (it = v.begin(); it != v.end(); ++it) {
        std::cout << *it << " ";
    }
    return 0;
}
```

---

## **정리**
✅ **STL은 컨테이너 + 알고리즘 + 반복자로 이루어진 강력한 라이브러리**
✅ **일반적인 자료구조와 알고리즘을 쉽게 활용할 수 있도록 제공**
✅ **반복자와 함수 객체를 활용하여 유연한 코드 작성 가능**

📌 **실전 개발에서 STL을 적극 활용하면 코드의 효율성과 가독성이 크게 향상됨!**