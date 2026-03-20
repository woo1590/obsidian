# 📌 C++ STL - `map` 정리

## ✅ `map` 기본 사용법
```cpp
#include <map>  // 헤더파일 포함해야 사용 가능

int main() {
    std::map<int, int> mapInt; 
    
    mapInt.insert(std::make_pair(1, 100)); // 가능 (pair 객체 사용)
    
    for (std::map<int, int>::iterator iter = mapInt.begin(); iter != mapInt.end(); ++iter) {
        std::cout << iter->first << " : " << iter->second << std::endl;
    }
}
```

- `map`은 **pair 객체**를 원소로 가지므로, `(*iter).first`, `(*iter).second` 또는 `iter->first`, `iter->second`로 접근해야 함.
- `map`은 자동정렬을 지원하기 때문에 정렬 방식에 대한 `조건자`를 선언시에 넣을 수 있음. 

---

## ✅ `map` 원소 추가 방법

### 1️⃣ `pair` 객체를 직접 생성하여 추가
```cpp
std::pair<int, int> MyPair(1, 100);
mapInt.insert(MyPair);
```

### 2️⃣ `pair` 임시 객체 사용
```cpp
mapInt.insert(std::pair<int, int>(2, 200));
```

### 3️⃣ `make_pair` 함수 사용 (추천)
```cpp
mapInt.insert(std::make_pair(3, 300));
```

### 4️⃣ `value_type` 사용
```cpp
std::map<int, int>::value_type MyValue(4, 400);
mapInt.insert(MyValue);
```

### 5️⃣ `value_type` 임시 객체 사용
```cpp
mapInt.insert(std::map<int, int>::value_type(5, 500));
```

### 6️⃣ `[]` 연산자 사용 (주의!)
```cpp
mapInt[6] = 600;
```
- **`insert`와 차이점**
  - `insert`는 중복된 키가 있으면 추가되지 않음.
  - `[]` 연산자는 키가 존재하면 **기존 값을 덮어씀**.

### 7️⃣ 모던 C++ (`C++11` 이상)
#### 🔹 유니폼 초기화 사용
```cpp
mapInt.insert({7, 700});
```
#### 🔹 `emplace` 사용 (추천)
```cpp
mapInt.emplace(8, 800);
```
- `insert`는 **`pair` 객체를 먼저 생성한 후 삽입**, `emplace`는 **직접 생성**하여 더 효율적임.

---

## ✅ `map`의 반복자
- **양방향 반복자 지원 (`++`, `--` 가능)**

```cpp
std::map<int, int>::iterator iter = mapInt.begin();
iter++;
iter++;
iter--;

mapInt.insert({10, 1000}); // 자동 정렬되므로 중간 삽입은 의미 없음

mapInt.erase(iter);   // 특정 위치의 원소 삭제
mapInt.erase(4);      // key 값으로 삭제 가능
```

---

## ✅ `map`과 `find_if`
```cpp
#include <iostream>
#include <map>
#include <cstring>
#include <algorithm>

struct tagFinder {
    tagFinder(const char* pTag) : m_pTag(pTag) {}
    
    template<typename T>
    bool operator()(const T& MyPair) const {
        return !strcmp(m_pTag, MyPair.first);
    }
    
    const char* m_pTag;
};

int main() {
    std::map<const char*, int, bool(*)(const char*, const char*)> myMap(
        [](const char* a, const char* b) { return strcmp(a, b) < 0; }
    );

    myMap.insert({"aaa", 100});
    myMap.insert({"bbb", 200});
    myMap.insert({"ccc", 300});

    // 일반 find (주소 비교로 인해 비정상적인 결과 가능)
    auto iter = myMap.find("bbb");

    // find_if를 사용한 문자열 비교
    iter = std::find_if(myMap.begin(), myMap.end(), tagFinder("bbb"));

    if (iter != myMap.end()) {
        std::cout << "찾은 값: " << iter->second << std::endl;
    } else {
        std::cout << "찾지 못함\n";
    }
    return 0;
}
```

### **🚨 `map<const char*, int>`의 문제점**
- `const char*`을 키로 사용하면 **주소 값으로 비교**하므로 `"bbb"`를 제대로 찾지 못할 수도 있음.
- 해결법:
  1. **`std::string`을 키로 사용** (권장)
  2. **`strcmp`를 이용한 비교자 추가**

---

## ✅ **`map`의 정렬 방식**
| Key 타입  | 정렬 기준 |
|-----------|-----------------------------------|
| `char`    | O (ASCII 코드 순서대로 정렬)     |
| `char*`   | X (주소 값 기준 정렬)             |
| `string`  | O (`operator<`가 알파벳 기준 정렬) |


📌 **정리:** `map`을 사용할 때 `const char*`보다 `std::string`을 쓰는 것이 안전함!

