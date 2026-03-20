```cpp
#include <vector>   // 헤더파일 포함
#include <iostream>

int main() {
    std::vector<int> intVec;

    // 원소 추가
    intVec.push_back(10);
    intVec.push_back(20);
    intVec.push_back(30);

    // 반복자를 사용한 출력
    for (std::vector<int>::iterator iter = intVec.begin(); iter != intVec.end(); ++iter) {
        std::cout << *iter << std::endl;
    }

    // 인덱스를 이용한 접근도 가능
    std::cout << intVec[0] << std::endl;

    return 0;
}

```
------------------------------------------------

### 📌특징
- 동적 배열의 구조를 C++로 구현
- `임의 접근(random access)`이 가능함
- **메모리 연속성 보장(캐시 성능 좋음)
- 맨 뒤에 원소 삽입 시 O(1) 으로  빠르지만 앞이나 중간 삽입 시 O(n) 소요
- 할당한 메모리 공간 보다 더 많은 원소 삽입 시 새로운 메모리 할당, 원소 복사가 일어나게 됨
------------------------------------------------

### 📌멤버 함수

**push_back(val)
- 맨 뒤에 원소를 추가
- 필요시 capacity 증가

**pop_back()
- 맨 뒤의 원소를 제거

**size()
- 현재 저장된 원소의 개수

**capacity()
- 실제 할당된 메모리 크기

**resize(n)
- 크기를 n으로 조절
- 자동으로 초기화 됨

**reserve(n)
- n만큼 capacity 할당
- 자동으로 원소를 채우지 않음

**at(index)
- 안전한 인덱스 접근
- 범위를 벗어나면 예외 발생

**insert(iter,val)
- `iter`가 가리키는 위치에 원소 삽입
- 중간 삽입 시 O(n)소요

**erase(iter)
- `iter` 위치의 원소 제거
- `erase(start, end)`로 범위 제거 가능