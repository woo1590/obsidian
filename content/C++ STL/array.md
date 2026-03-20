`#include <array>`
기존에 사용하던 정적 배열을 객체화
생성자, 소멸자, 복사 생성자, 대입 연사자를 지원하여 객체 지향다운 배열 사용이 가능

```cpp
//기존 배열
int iArray[5]={1,2,3,4,5};
array<int,5> arrEx={1,2,3,4,5};

//배열 크기
cout<<sizeof(iArray)/sizeof(int);
cout<<arrEx.size();

//배열간의 대입
int iTemp[5]={};
iTemp=iArray;  //불가능

array<int,5> arrTmp={};
arrTmp=arrEx;  //가능
```
------------------------
### 특징
- 기존 컨테이너와 마찬가지로 empty, swap, front, back 함수 제공
- 삽입, 삭제의 동적인 함수들은 제공하지 않음(push_back, insert, pop, clear)
----------------------------------

**data()
- 배열의 첫 주소를 반환하는 함수
```
int *p = arrEx.data();
```

**fill(val)
- 배열의 모든 원소를 val로 채우는 함수
```
arrEx.fill(0);  //모든 원소가 0으로 채워짐
```


**vector와 array
- 크기가 확실히 정해져 있다면 array 사용을 고려해볼만하다
- 동적인 상황이 많은 게임에서는 vector의 빈도가 높음