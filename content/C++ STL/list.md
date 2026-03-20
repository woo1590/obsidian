```cpp
#include <list>    // 헤더파일 포함해야 사용 가능
#include <iostream>

int main() {
    std::list<int> intlist;
    
    // 원소 추가
    intlist.push_back(1);
    intlist.push_back(2);
    intlist.push_back(3);
    intlist.push_back(4);
    intlist.push_back(5);
    
    // 반복자를 사용하여 출력
    for (std::list<int>::iterator iter = intlist.begin(); iter != intlist.end(); ++iter) {
        std::cout << (*iter) << std::endl;
    }
    return 0;
}
```

### 📌 특징
- **vector와 다르게 반복자를 통해서만 접근이 가능**하다.

---

### **📌 멤버 함수 정리**

#### **sort()**
- STL 알고리즘의 `sort()` 함수를 사용할 수 없기 때문에 **멤버 함수로 제공**
- `greater<>`, `less<>` 등 **조건자를 사용하여 정렬 가능**

#### **reverse()**
- 원소들의 순서를 **역순으로 변경**하는 함수
- 📌 예시: **길찾기 알고리즘 시 활용 가능**[^1]

#### **remove(val)**
- `val` 값과 일치하는 원소를 제거하는 함수

#### **remove_if(조건자)**
- 특정 조건과 **일치하는 원소를 제거**하는 함수

#### **splice(iter, list)**
- 잘라내기 & 붙여넣기 함수
- `iter`가 가리키는 위치에 인자로 들어온 `list`를 붙여넣음[^2]

---

[^1]: 좀 더 찾아서 정리 필요
[^2]: 기존 리스트에서 지정된 부분을 잘라낸 후 붙여넣음

